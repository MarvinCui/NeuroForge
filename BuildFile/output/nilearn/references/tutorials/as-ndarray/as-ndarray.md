# How To: As Ndarray

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test as ndarray

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `nilearn._utils.numpy_conversions`

**Setup Required:**
```python
# Fixtures: input_dtype, input_order, copy, output_dtype, output_order, was_copied
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (10, 11)
```

**Verification:**
```python
assert are_arrays_identical(arr1[0], arr2[0]) != was_copied
```

### Step 2: Assign arr1 = np.ones(...)

```python
arr1 = np.ones(shape, dtype=input_dtype, order=input_order)
```

**Verification:**
```python
assert arr2.dtype == input_dtype
```

### Step 3: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, copy=copy, dtype=output_dtype, order=output_order)
```

**Verification:**
```python
assert arr2.dtype == output_dtype
```

### Step 4: Assign result_order = value

```python
result_order = output_order if output_order is not None else input_order
```

**Verification:**
```python
assert arr2.flags['F_CONTIGUOUS']
```


## Complete Example

```python
# Setup
# Fixtures: input_dtype, input_order, copy, output_dtype, output_order, was_copied

# Workflow
shape = (10, 11)
arr1 = np.ones(shape, dtype=input_dtype, order=input_order)
arr2 = as_ndarray(arr1, copy=copy, dtype=output_dtype, order=output_order)
assert are_arrays_identical(arr1[0], arr2[0]) != was_copied
if output_dtype is None:
    assert arr2.dtype == input_dtype
else:
    assert arr2.dtype == output_dtype
result_order = output_order if output_order is not None else input_order
if result_order == 'F':
    assert arr2.flags['F_CONTIGUOUS']
else:
    assert arr2.flags['C_CONTIGUOUS']
```

## Next Steps


---

*Source: test_numpy_conversions.py:124 | Complexity: Intermediate | Last updated: 2026-05-18*