# How To: Reconst Ivim

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: test reconst ivim

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.io.image`
- `dipy.sims.voxel`
- `dipy.workflows.reconst`


## Step-by-Step Guide

### Step 1: Assign bvals = np.array(...)

```python
bvals = np.array([0.0, 10.0, 20.0, 30.0, 40.0, 60.0, 80.0, 100.0, 120.0, 140.0, 160.0, 180.0, 200.0, 300.0, 400.0, 500.0, 600.0, 700.0, 800.0, 900.0, 1000.0])
```


## Complete Example

```python
# Workflow
bvals = np.array([0.0, 10.0, 20.0, 30.0, 40.0, 60.0, 80.0, 100.0, 120.0, 140.0, 160.0, 180.0, 200.0, 300.0, 400.0, 500.0, 600.0, 700.0, 800.0, 900.0, 1000.0])
```

## Next Steps


---

*Source: test_reconst_ivim.py:16 | Complexity: Beginner | Last updated: 2026-05-18*