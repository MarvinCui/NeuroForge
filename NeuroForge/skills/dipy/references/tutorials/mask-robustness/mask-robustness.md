# How To: Mask Robustness

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that auto-mask and manual mask give similar results.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise.bias_correction`
- `dipy.segment.mask`
- `math`


## Step-by-Step Guide

### Step 1: 'Test that auto-mask and manual mask give similar results.'

```python
'Test that auto-mask and manual mask give similar results.'
```

**Verification:**
```python
assert corr > 0.9, f'Auto vs manual mask correlation too low: {corr:.4f}'
```

### Step 2: Assign unknown = _make_synthetic_dwi(...)

```python
data, gtab, _, true_mask = _make_synthetic_dwi()
```

### Step 3: Assign unknown = bias_field_correction(...)

```python
_, bf_auto = bias_field_correction(data, gtab, mask=None, method='poly', pyramid_levels=(2, 1), n_iter=2, robust=False, gradient_weighting=False, return_bias_field=True)
```

### Step 4: Assign unknown = bias_field_correction(...)

```python
_, bf_manual = bias_field_correction(data, gtab, mask=true_mask, method='poly', pyramid_levels=(2, 1), n_iter=2, robust=False, gradient_weighting=False, return_bias_field=True)
```

### Step 5: Assign bf_a = unknown.ravel(...)

```python
bf_a = bf_auto[true_mask].ravel()
```

### Step 6: Assign bf_m = unknown.ravel(...)

```python
bf_m = bf_manual[true_mask].ravel()
```

### Step 7: Assign corr = value

```python
corr = np.corrcoef(bf_a, bf_m)[0, 1]
```

**Verification:**
```python
assert corr > 0.9, f'Auto vs manual mask correlation too low: {corr:.4f}'
```


## Complete Example

```python
# Workflow
'Test that auto-mask and manual mask give similar results.'
data, gtab, _, true_mask = _make_synthetic_dwi()
_, bf_auto = bias_field_correction(data, gtab, mask=None, method='poly', pyramid_levels=(2, 1), n_iter=2, robust=False, gradient_weighting=False, return_bias_field=True)
_, bf_manual = bias_field_correction(data, gtab, mask=true_mask, method='poly', pyramid_levels=(2, 1), n_iter=2, robust=False, gradient_weighting=False, return_bias_field=True)
bf_a = bf_auto[true_mask].ravel()
bf_m = bf_manual[true_mask].ravel()
corr = np.corrcoef(bf_a, bf_m)[0, 1]
assert corr > 0.9, f'Auto vs manual mask correlation too low: {corr:.4f}'
```

## Next Steps


---

*Source: test_bias_correction.py:448 | Complexity: Intermediate | Last updated: 2026-05-18*