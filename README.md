# Module 3 - Pairwise alignment (part 1)
## 3.1. Making and interpreting dotplots
In this exercise, you will be working in your groups to generate a dotplot and interpreting it together. To make the dotplot, you will be using an online tool called Dotmatcher. You will pick the sequences to use yourself. The actual dotplot should be uploaded to Canvas together with your description. Your group is finished with the exercise when you have uploaded a dotplot and your (textual) interpretation of it, and gotten it approved by the teacher. 

It is probably best if each of you first work on your own to identify interesting pairs of sequences, and then decide in the group which one to go for in the end. *Each group uploads one dotplot and one interpretation text.*

- Go to this [canvas discussion](https://uio.instructure.com/courses/55156/discussion_topics/415914) and follow the instructions there. 
- Your group's answer should be posted to the Canvas discussion board (click 'Svar').
- When your group's answer is read and approved, you can proceed to the next exercise

## 3.2 Doing pairwise sequence alignment manually
In this exercise, you will be working in your groups to manually generate a pairwise sequence alignment. To do this, **each person in the group** draws up an alignment matrix and fills it in with the numbers and arrows between the cells. Indicate (using color or another way of higlighting) the backtracing of the optimal alignment(s). It is probably smart to find a piece of paper to draft your individual solutions. You can then either take picture of your piece of paper, or use a drawing tool. Feel free to share results with others in the group to compare your answers and verify whether they seem identical and correct.
- Go to this [canvas discussion](https://uio.instructure.com/courses/55156/discussion_topics/415913) for further instructions on the exercise and to deliver your group's answers
- When your group's answer is read and approved, you can proceed to the next exercise
- For python code, use the following code as inspiration. Modify the code according to your group's exercise. Use the code to check that your group's answer is correct:
```python
from Bio import Align
aligner = Align.PairwiseAligner()
aligner.mode = 'global'
aligner.match_score = 2
aligner.mismatch_score = -1
aligner.gap_score = -2
alignments = aligner.align("TACCG", "ACG")
for alignment in alignments:
  print("Score = %.1f:" % alignment.score)
  print(alignment)
```

## 3.3 Making a simple dotplot-like tool
With this python code, you can make an empty matrix (filled with 0) of size `n` by `m`, where  `n` and `m` are lengths of sequences `a` and `b`:
```python
a = "AAAT"
b = "GAT"
n = len(a)
m = len(b)
matrix = [ [ 0 for j in range(m) ] for i in range(n) ]
```
Note that `matrix` is just a list-of-lists. To access elements in `matrix`, you do the same as for lists, except that now there is a list inside the list. Thus, to access the the element in row 0 and column 3, you can do like this: `matrix[0][3]`. Thus, to access all elements in the matrix, and for example print these, we can do like this:

```python
for i in range(n):
  for j in range(m):
    print(matrix[i][j])
```

To print the final matrix, we can do like this:
```python
for row in matrix:
    print(row)
```

When we use a for-loop within another for-loop, we call this a **nested loop**.

```diff
! Explain the logic of the nested for-loop above
! Create a Python script that fills the matrix with 1 whenever the bases match, and 0 otherwise
! Save the script in `dotplot.py`, and make it so that it prints the filled-out matrix
```

## 3.4 Using Python code to fill out the alignment matrix
In this exercise, we will start creating our own implementation of the Needleman-Wunsch algorithm, by building on existing code (see below) to generate the alignment matrix.

We can modify and extend the above code to create an empty alignment matrix:
```python
a = "AAAT"
b = "GAT"
n = len(a)
m = len(b)

match = 1
mismatch = -1
gap = -2

matrix = [ [ 0 for j in range(m+1) ] for i in range(n+1) ] # create and fill matrix with 0s

# Fill the first row with gap scores:
for i in range(1,n+1):
  matrix[i][0] = gap*i

# Fill the first column with gap scores:
for j in range(1,m+1):
  matrix[0][j] = gap*j
```

```diff
! Explain why the matrix needs to be initialized like this
```

Here are the building blocks you need to make an implementation of the Needleman-Wunsch (and Smith-Waterman) algorithm for filling out the alignment matrix:

```python
for i in range(1,n+1):
  for j in range(1,m+1):
    score_left = matrix[i][j-1]
    score_above = ...
    score_diagonal = ...
    if a[i-1] == b[j-1]: # A match between elements in the sequences
      score_diagonal += ...
    else: # A mismatch between the elements 
      score_diagonal += ...      
    
    # Always add gap penalty to scores from left or above:
    score_left += ...
    score_above += ...
    
    # Find the highest score and insert that score to the matrix:
    score = max(...)
    matrix[i][j] = score

# print each row in the matrix and check that it makes sense
for row in matrix:
    print(row)
```

```diff
+ Hint:
+ max(6,2,-1) returns the maximum value (6 in this case)
```

```diff
! Fill in all places with `...` to create a alignment matrix with correct alignment scores
! Verify manually that your code outputs the correct matrix
! Modify your code to work with local alignments as well
```


## 3.5 Advanced (and optional) exercise
```diff
! Extend the code to do the back-tracing and to generate the sequence alignments
```
