# How To: Synthetic Bspline Bias Rmse

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that B-spline estimated bias field correlates with true field.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise.bias_correction`
- `dipy.segment.mask`
- `math`


## Step-by-Step Guide

### Step 1: 'Test that B-spline estimated bias field correlates with true field.'

```python
'Test that B-spline estimated bias field correlates with true field.'
```

**Verification:**
```python
assert rmse < 0.5, f'B-spline bias RMSE too large: {rmse:.4f}'
```

### Step 2: Assign unknown = _make_synthetic_dwi(...)

```python
data, gtab, true_bias, mask = _make_synthetic_dwi(shape=(20, 20, 15), n_vols=10)
```

### Step 3: Assign unknown = bias_field_correction(...)

```python
_, bias_field = bias_field_correction(data, gtab, mask=mask, method='bspline', n_control_points=(4, 4, 3), pyramid_levels=(4, 2, 1), n_iter=4, robust=True, gradient_weighting=True, return_bias_field=True)
```

### Step 4: Assign bf_norm = value

```python
bf_norm = bias_field[mask] / bias_field[mask].mean()
```

### Step 5: Assign true_norm = value

```python
true_norm = true_bias[mask] / true_bias[mask].mean()
```

### Step 6: Assign rmse = np.sqrt(...)

```python
rmse = np.sqrt(np.mean((bf_norm - true_norm) ** 2))
```

**Verification:**
```python
assert rmse < 0.5, f'B-spline bias RMSE too large: {rmse:.4f}'
```


## Complete Example

```python
# Workflow
'Test that B-spline estimated bias field correlates with true field.'
data, gtab, true_bias, mask = _make_synthetic_dwi(shape=(20, 20, 15), n_vols=10)
_, bias_field = bias_field_correction(data, gtab, mask=mask, method='bspline', n_control_points=(4, 4, 3), pyramid_levels=(4, 2, 1), n_iter=4, robust=True, gradient_weighting=True, return_bias_field=True)
bf_norm = bias_field[mask] / bias_field[mask].mean()
true_norm = true_bias[mask] / true_bias[mask].mean()
rmse = np.sqrt(np.mean((bf_norm - true_norm) ** 2))
assert rmse < 0.5, f'B-spline bias RMSE too large: {rmse:.4f}'
```

## Next Steps


---

*Source: test_bias_correction.py:268 | Complexity: Intermediate | Last updated: 2026-05-18*