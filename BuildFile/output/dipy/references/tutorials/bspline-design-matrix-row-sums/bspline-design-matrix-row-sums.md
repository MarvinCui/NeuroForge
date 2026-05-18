# How To: Bspline Design Matrix Row Sums

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bspline design matrix row sums

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
assert row_sums.min() > 0.0
```

### Step 2: Assign n_ctrl = value

```python
n_ctrl = (4, 4, 3)
```

**Verification:**
```python
assert row_sums.max() <= 1.1
```

### Step 3: Assign mask = np.ones(...)

```python
mask = np.ones(shape, dtype=bool)
```

### Step 4: Assign X = _build_bspline_design_matrix(...)

```python
X = _build_bspline_design_matrix(log_b0_shape=shape, n_control=n_ctrl, mask_flat=mask.ravel())
```

### Step 5: Assign row_sums = np.asarray.ravel(...)

```python
row_sums = np.asarray(X.sum(axis=1)).ravel()
```

**Verification:**
```python
assert row_sums.min() > 0.0
```


## Complete Example

```python
# Workflow
shape = (10, 10, 8)
n_ctrl = (4, 4, 3)
mask = np.ones(shape, dtype=bool)
X = _build_bspline_design_matrix(log_b0_shape=shape, n_control=n_ctrl, mask_flat=mask.ravel())
row_sums = np.asarray(X.sum(axis=1)).ravel()
assert row_sums.min() > 0.0
assert row_sums.max() <= 1.1
```

## Next Steps


---

*Source: test_bias_correction.py:186 | Complexity: Intermediate | Last updated: 2026-05-18*