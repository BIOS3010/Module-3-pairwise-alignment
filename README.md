# Module-3-pairwise-alignment
**1. Dotplot***
**2. Needleman-Wunch manually***
**3. Compare with result from Biopython***
```python
from Bio import Align
aligner = Align.PairwiseAligner()
alignments = aligner.align("TACCG", "ACG")
```
