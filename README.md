# Module-3-pairwise-alignment
**1. Dotplots**
- Each breakout-group gets a different dotplot on padlet (alternative: draw a dotplot)
- Interpret in group
- Load answer to padlet
**2. Needleman-Wunch manually**
- Each breakout-group gets a pair of sequences. 
- Everyone does a manual Needleman-Wunch alignment
- Compare with each other to make sure 
- load answer to padlet
**3. Compare with result from Biopython**
```python
from Bio import Align
aligner = Align.PairwiseAligner()
alignments = aligner.align("TACCG", "ACG")
```
