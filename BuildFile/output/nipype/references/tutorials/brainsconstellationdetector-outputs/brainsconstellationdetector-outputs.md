# How To: Brainsconstellationdetector Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSConstellationDetector outputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(outputLandmarksInACPCAlignedSpace=dict(extensions=None), outputLandmarksInInputSpace=dict(extensions=None), outputMRML=dict(extensions=None), outputResampledVolume=dict(extensions=None), outputTransform=dict(extensions=None), outputUntransformedClippedVolume=dict(extensions=None), outputVerificationScript=dict(extensions=None), outputVolume=dict(extensions=None), resultsDir=dict(), writeBranded2DImage=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(outputLandmarksInACPCAlignedSpace=dict(extensions=None), outputLandmarksInInputSpace=dict(extensions=None), outputMRML=dict(extensions=None), outputResampledVolume=dict(extensions=None), outputTransform=dict(extensions=None), outputUntransformedClippedVolume=dict(extensions=None), outputVerificationScript=dict(extensions=None), outputVolume=dict(extensions=None), resultsDir=dict(), writeBranded2DImage=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_BRAINSConstellationDetector.py:165 | Complexity: Beginner | Last updated: 2026-05-18*