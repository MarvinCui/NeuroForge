# How To: Brainextraction Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BrainExtraction outputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(BrainExtractionBrain=dict(extensions=None), BrainExtractionCSF=dict(extensions=None), BrainExtractionGM=dict(extensions=None), BrainExtractionInitialAffine=dict(extensions=None), BrainExtractionInitialAffineFixed=dict(extensions=None), BrainExtractionInitialAffineMoving=dict(extensions=None), BrainExtractionLaplacian=dict(extensions=None), BrainExtractionMask=dict(extensions=None), BrainExtractionPrior0GenericAffine=dict(extensions=None), BrainExtractionPrior1InverseWarp=dict(extensions=None), BrainExtractionPrior1Warp=dict(extensions=None), BrainExtractionPriorWarped=dict(extensions=None), BrainExtractionSegmentation=dict(extensions=None), BrainExtractionTemplateLaplacian=dict(extensions=None), BrainExtractionTmp=dict(extensions=None), BrainExtractionWM=dict(extensions=None), N4Corrected0=dict(extensions=None), N4Truncated0=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(BrainExtractionBrain=dict(extensions=None), BrainExtractionCSF=dict(extensions=None), BrainExtractionGM=dict(extensions=None), BrainExtractionInitialAffine=dict(extensions=None), BrainExtractionInitialAffineFixed=dict(extensions=None), BrainExtractionInitialAffineMoving=dict(extensions=None), BrainExtractionLaplacian=dict(extensions=None), BrainExtractionMask=dict(extensions=None), BrainExtractionPrior0GenericAffine=dict(extensions=None), BrainExtractionPrior1InverseWarp=dict(extensions=None), BrainExtractionPrior1Warp=dict(extensions=None), BrainExtractionPriorWarped=dict(extensions=None), BrainExtractionSegmentation=dict(extensions=None), BrainExtractionTemplateLaplacian=dict(extensions=None), BrainExtractionTmp=dict(extensions=None), BrainExtractionWM=dict(extensions=None), N4Corrected0=dict(extensions=None), N4Truncated0=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_BrainExtraction.py:71 | Complexity: Beginner | Last updated: 2026-05-18*