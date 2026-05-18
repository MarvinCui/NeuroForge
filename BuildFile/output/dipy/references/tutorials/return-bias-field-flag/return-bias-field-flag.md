# How To: Return Bias Field Flag

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test return_bias_field=True returns tuple, False returns array.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise.bias_correction`
- `dipy.segment.mask`
- `math`


## Step-by-Step Guide

### Step 1: 'Test return_bias_field=True returns tuple, False returns array.'

```python
'Test return_bias_field=True returns tuple, False returns array.'
```

**Verification:**
```python
assert isinstance(result, tuple)
```

### Step 2: Assign unknown = _make_synthetic_dwi(...)

```python
data, gtab, _, mask = _make_synthetic_dwi()
```

**Verification:**
```python
assert len(result) == 2
```

### Step 3: Assign result = bias_field_correction(...)

```python
result = bias_field_correction(data, gtab, mask=mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=True)
```

**Verification:**
```python
assert corrected.shape == data.shape
```

### Step 4: Assign unknown = result

```python
corrected, bias_field = result
```

**Verification:**
```python
assert bias_field.shape == data.shape[:3]
```

### Step 5: Assign result_nodfield = bias_field_correction(...)

```python
result_nodfield = bias_field_correction(data, gtab, mask=mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=False)
```

**Verification:**
```python
assert isinstance(result_nodfield, np.ndarray)
```


## Complete Example

```python
# Workflow
'Test return_bias_field=True returns tuple, False returns array.'
data, gtab, _, mask = _make_synthetic_dwi()
result = bias_field_correction(data, gtab, mask=mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=True)
assert isinstance(result, tuple)
assert len(result) == 2
corrected, bias_field = result
assert corrected.shape == data.shape
assert bias_field.shape == data.shape[:3]
result_nodfield = bias_field_correction(data, gtab, mask=mask, method='poly', pyramid_levels=(2, 1), n_iter=1, robust=False, gradient_weighting=False, return_bias_field=False)
assert isinstance(result_nodfield, np.ndarray)
```

## Next Steps


---

*Source: test_bias_correction.py:388 | Complexity: Intermediate | Last updated: 2026-05-18*