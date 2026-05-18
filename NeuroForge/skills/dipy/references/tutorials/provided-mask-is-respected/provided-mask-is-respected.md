# How To: Provided Mask Is Respected

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that a provided mask restricts correction to the given region.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise.bias_correction`
- `dipy.segment.mask`
- `math`


## Step-by-Step Guide

### Step 1: 'Test that a provided mask restricts correction to the given region.'

```python
'Test that a provided mask restricts correction to the given region.'
```

### Step 2: Assign unknown = _make_synthetic_dwi(...)

```python
data, gtab, _, full_mask = _make_synthetic_dwi()
```

### Step 3: Assign upper_mask = full_mask.copy(...)

```python
upper_mask = full_mask.copy()
```

### Step 4: Assign unknown = False

```python
upper_mask[data.shape[0] // 2:] = False
```

### Step 5: Assign unknown = bias_field_correction(...)

```python
corrected, _ = bias_field_correction(data, gtab, mask=upper_mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=True)
```

### Step 6: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(corrected[~upper_mask], 0)
```


## Complete Example

```python
# Workflow
'Test that a provided mask restricts correction to the given region.'
data, gtab, _, full_mask = _make_synthetic_dwi()
upper_mask = full_mask.copy()
upper_mask[data.shape[0] // 2:] = False
corrected, _ = bias_field_correction(data, gtab, mask=upper_mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=True)
np.testing.assert_array_equal(corrected[~upper_mask], 0)
```

## Next Steps


---

*Source: test_bias_correction.py:614 | Complexity: Intermediate | Last updated: 2026-05-18*