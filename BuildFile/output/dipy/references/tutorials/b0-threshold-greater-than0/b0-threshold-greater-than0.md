# How To: B0 Threshold Greater Than0

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Added test case for default b0_threshold set to 50.
Checks if error is thrown correctly.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.reconst.ivim`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: '\n    Added test case for default b0_threshold set to 50.\n    Checks if error is thrown correctly.\n    '

```python
'\n    Added test case for default b0_threshold set to 50.\n    Checks if error is thrown correctly.\n    '
```

**Verification:**
```python
assert b0_s in vae.exception
```

### Step 2: Assign bvals_b0t = np.array(...)

```python
bvals_b0t = np.array([50.0, 10.0, 20.0, 30.0, 40.0, 60.0, 80.0, 100.0, 120.0, 140.0, 160.0, 180.0, 200.0, 300.0, 400.0, 500.0, 600.0, 700.0, 800.0, 900.0, 1000.0])
```

### Step 3: Assign N = len(...)

```python
N = len(bvals_b0t)
```

### Step 4: Assign bvecs = generate_bvecs(...)

```python
bvecs = generate_bvecs(N)
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals_b0t, bvecs=bvecs.T)
```

### Step 6: Assign _ = IvimModel(...)

```python
_ = IvimModel(gtab, fit_method='trr')
```

### Step 7: Assign b0_s = 'The IVIM model requires a measurement at b==0. As of '

```python
b0_s = 'The IVIM model requires a measurement at b==0. As of '
```

**Verification:**
```python
assert b0_s in vae.exception
```


## Complete Example

```python
# Workflow
'\n    Added test case for default b0_threshold set to 50.\n    Checks if error is thrown correctly.\n    '
bvals_b0t = np.array([50.0, 10.0, 20.0, 30.0, 40.0, 60.0, 80.0, 100.0, 120.0, 140.0, 160.0, 180.0, 200.0, 300.0, 400.0, 500.0, 600.0, 700.0, 800.0, 900.0, 1000.0])
N = len(bvals_b0t)
bvecs = generate_bvecs(N)
gtab = gradient_table(bvals_b0t, bvecs=bvecs.T)
with assert_raises(ValueError) as vae:
    _ = IvimModel(gtab, fit_method='trr')
    b0_s = 'The IVIM model requires a measurement at b==0. As of '
    assert b0_s in vae.exception
```

## Next Steps


---

*Source: test_ivim.py:333 | Complexity: Advanced | Last updated: 2026-05-18*