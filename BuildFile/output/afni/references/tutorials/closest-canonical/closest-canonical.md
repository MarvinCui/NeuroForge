# How To: Closest Canonical

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test closest canonical

## Prerequisites

**Required Modules:**
- `__future__`
- `numpy`
- `funcs`
- `nifti1`
- `loadsave`
- `tmpdirs`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24).reshape((2, 3, 4, 1))
```

**Verification:**
```python
assert_true(img is xyz_img)
```

### Step 2: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, np.eye(4))
```

**Verification:**
```python
assert_false(img is xyz_img)
```

### Step 3: Assign xyz_img = as_closest_canonical(...)

```python
xyz_img = as_closest_canonical(img)
```

**Verification:**
```python
assert_array_equal(out_arr, np.flipud(arr))
```

### Step 4: Call assert_true()

```python
assert_true(img is xyz_img)
```

**Verification:**
```python
assert_true(img is xyz_img)
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, np.diag([-1, 1, 1, 1]))
```

**Verification:**
```python
assert_raises(OrientationError, as_closest_canonical, img, True)
```

### Step 6: Assign xyz_img = as_closest_canonical(...)

```python
xyz_img = as_closest_canonical(img)
```

### Step 7: Call assert_false()

```python
assert_false(img is xyz_img)
```

### Step 8: Assign out_arr = xyz_img.get_data(...)

```python
out_arr = xyz_img.get_data()
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(out_arr, np.flipud(arr))
```

### Step 10: Assign xyz_img = as_closest_canonical(...)

```python
xyz_img = as_closest_canonical(img, True)
```

### Step 11: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

### Step 12: Assign unknown = 0.1

```python
aff[0, 1] = 0.1
```

### Step 13: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

### Step 14: Assign xyz_img = as_closest_canonical(...)

```python
xyz_img = as_closest_canonical(img)
```

### Step 15: Call assert_true()

```python
assert_true(img is xyz_img)
```

### Step 16: Call assert_raises()

```python
assert_raises(OrientationError, as_closest_canonical, img, True)
```


## Complete Example

```python
# Workflow
arr = np.arange(24).reshape((2, 3, 4, 1))
img = Nifti1Image(arr, np.eye(4))
xyz_img = as_closest_canonical(img)
assert_true(img is xyz_img)
img = Nifti1Image(arr, np.diag([-1, 1, 1, 1]))
xyz_img = as_closest_canonical(img)
assert_false(img is xyz_img)
out_arr = xyz_img.get_data()
assert_array_equal(out_arr, np.flipud(arr))
xyz_img = as_closest_canonical(img, True)
aff = np.eye(4)
aff[0, 1] = 0.1
img = Nifti1Image(arr, aff)
xyz_img = as_closest_canonical(img)
assert_true(img is xyz_img)
assert_raises(OrientationError, as_closest_canonical, img, True)
```

## Next Steps


---

*Source: test_funcs.py:63 | Complexity: Advanced | Last updated: 2026-05-18*