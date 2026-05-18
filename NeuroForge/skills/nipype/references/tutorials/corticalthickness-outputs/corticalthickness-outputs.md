# How To: Corticalthickness Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CorticalThickness outputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(BrainExtractionMask=dict(extensions=None), BrainSegmentation=dict(extensions=None), BrainSegmentationN4=dict(extensions=None), BrainSegmentationPosteriors=dict(), BrainVolumes=dict(extensions=None), CorticalThickness=dict(extensions=None), CorticalThicknessNormedToTemplate=dict(extensions=None), ExtractedBrainN4=dict(extensions=None), SubjectToTemplate0GenericAffine=dict(extensions=None), SubjectToTemplate1Warp=dict(extensions=None), SubjectToTemplateLogJacobian=dict(extensions=None), TemplateToSubject0Warp=dict(extensions=None), TemplateToSubject1GenericAffine=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(BrainExtractionMask=dict(extensions=None), BrainSegmentation=dict(extensions=None), BrainSegmentationN4=dict(extensions=None), BrainSegmentationPosteriors=dict(), BrainVolumes=dict(extensions=None), CorticalThickness=dict(extensions=None), CorticalThicknessNormedToTemplate=dict(extensions=None), ExtractedBrainN4=dict(extensions=None), SubjectToTemplate0GenericAffine=dict(extensions=None), SubjectToTemplate1Warp=dict(extensions=None), SubjectToTemplateLogJacobian=dict(extensions=None), TemplateToSubject0Warp=dict(extensions=None), TemplateToSubject1GenericAffine=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_CorticalThickness.py:104 | Complexity: Beginner | Last updated: 2026-05-18*