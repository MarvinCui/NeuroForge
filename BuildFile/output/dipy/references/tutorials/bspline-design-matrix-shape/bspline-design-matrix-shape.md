# How To: Bspline Design Matrix Shape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bspline design matrix shape

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise.bias_correction`
- `dipy.segment.mask`
- `math`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (10, 10, 8)
```

**Verification:**
```python
assert X.shape == (N, K)
```

### Step 2: Assign n_ctrl = value

```python
n_ctrl = (4, 4, 3)
```

### Step 3: Assign mask = np.ones(...)

```python
mask = np.ones(shape, dtype=bool)
```

### Step 4: Assign X = _build_bspline_design_matrix(...)

```python
X = _build_bspline_design_matrix(log_b0_shape=shape, n_control=n_ctrl, mask_flat=mask.ravel())
```

### Step 5: Assign K = value

```python
K = n_ctrl[0] * n_ctrl[1] * n_ctrl[2]
```

### Step 6: Assign N = mask.sum(...)

```python
N = mask.sum()
```

**Verification:**
```python
assert X.shape == (N, K)
```


## Complete Example

```python
# Workflow
shape = (10, 10, 8)
n_ctrl = (4, 4, 3)
mask = np.ones(shape, dtype=bool)
X = _build_bspline_design_matrix(log_b0_shape=shape, n_control=n_ctrl, mask_flat=mask.ravel())
K = n_ctrl[0] * n_ctrl[1] * n_ctrl[2]
N = mask.sum()
assert X.shape == (N, K)
```

## Next Steps


---

*Source: test_bias_correction.py:174 | Complexity: Intermediate | Last updated: 2026-05-18*