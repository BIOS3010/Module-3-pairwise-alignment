# Module-3-pairwise-alignment
**3.1. Making and interpreting dotplots**
In this exercise, you will be working in your groups to generate a dotplot and interpreting it together. To make the dotplot, you will be using an online tool called Dotmatcher. You will pick the sequences to use yourself. The actual dotplot should be uploaded to Padlet together with your description. Your group is finished with the exercise when you have uploaded a dotplot and your (textual) interpretation of it. 

It is probably best if each of you first work on your own to identify interesting pairs of sequences, and then decide in the group which one to go for in the end. *Each group uploads one dotplot and one interpretation text.*

Do this:
- Go to the Padlet for this exercise: https://uio.padlet.org/jonaspaulsen/swu43yfx2vild7a9
- Look on the Example at the right side of the padlet for an example of how your group can deliver your results
- Go to https://www.ncbi.nlm.nih.gov/ and select "Protein"
- Search for the protein name listed under your group
- Pick two protein-sequences from two random organisms of your choice (avoid "partial" sequence)
- Copy the FASTA sequence from the two selected organisms (just the sequence, not the ID)
- Go to http://www.bioinformatics.nl/cgi-bin/emboss/dotmatcher and paste in your two selected sequences
- Use the default parameters, except that you should  add the X- and Y-axis title. The first pasted sequence ends up on the Y-axis, and the second ends up on the X-axis)
- Click `Run dotmatcher`, and save the result as a PNG.
- Load the PNG to the padlet
- Discuss the dotplot in the group and add your interpretation to the Padlet

**2. Needleman-Wunch manually**
- Each breakout-group gets a pair of sequences. 
- Everyone does a manual Needleman-Wunch alignment
- Compare with each other to make sure it is correct
- load one answer to padlet

**3. Compare with result from Biopython**
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
