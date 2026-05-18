# How To: Are Array Identical

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test are array identical

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `nilearn._utils.numpy_conversions`


## Step-by-Step Guide

### Step 1: Assign arr1 = np.ones(...)

```python
arr1 = np.ones(4)
```

**Verification:**
```python
assert are_arrays_identical(arr1, arr2)
```

### Step 2: Assign orig1 = arr1.copy(...)

```python
orig1 = arr1.copy()
```

**Verification:**
```python
assert are_arrays_identical(arr1, arr2)
```

### Step 3: Assign arr2 = arr1

```python
arr2 = arr1
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 4: Assign orig2 = arr2.copy(...)

```python
orig2 = arr2.copy()
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 5: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
```

### Step 6: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```

### Step 7: Assign arr2 = value

```python
arr2 = arr1[:1]
```

### Step 8: Assign orig2 = arr2.copy(...)

```python
orig2 = arr2.copy()
```

**Verification:**
```python
assert are_arrays_identical(arr1, arr2)
```

### Step 9: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
```

### Step 10: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```

### Step 11: Assign arr2 = value

```python
arr2 = arr1[1:]
```

### Step 12: Assign orig2 = arr2.copy(...)

```python
orig2 = arr2.copy()
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 13: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
```

### Step 14: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```

### Step 15: Assign arr2 = arr1.copy(...)

```python
arr2 = arr1.copy()
```

### Step 16: Assign orig2 = arr2.copy(...)

```python
orig2 = arr2.copy()
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 17: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
```

### Step 18: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```


## Complete Example

```python
# Workflow
arr1 = np.ones(4)
orig1 = arr1.copy()
arr2 = arr1
orig2 = arr2.copy()
assert are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1[:1]
orig2 = arr2.copy()
assert are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1[1:]
orig2 = arr2.copy()
assert not are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1.copy()
orig2 = arr2.copy()
assert not are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```

## Next Steps


---

*Source: test_numpy_conversions.py:43 | Complexity: Advanced | Last updated: 2026-05-18*