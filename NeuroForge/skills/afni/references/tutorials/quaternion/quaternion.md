# How To: Quaternion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quaternion

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert_true(np.allclose(hdr.get_qform_quaternion(), [1.0, 0, 0, 0]))
```

### Step 2: Assign unknown = 0

```python
hdr['quatern_b'] = 0
```

**Verification:**
```python
assert_true(np.allclose(hdr.get_qform_quaternion(), [0, 1, 0, 0]))
```

### Step 3: Assign unknown = 0

```python
hdr['quatern_c'] = 0
```

**Verification:**
```python
assert_array_almost_equal(hdr.get_qform_quaternion(), [0, 1, 0, 0])
```

### Step 4: Assign unknown = 0

```python
hdr['quatern_d'] = 0
```

### Step 5: Call assert_true()

```python
assert_true(np.allclose(hdr.get_qform_quaternion(), [1.0, 0, 0, 0]))
```

### Step 6: Assign unknown = 1

```python
hdr['quatern_b'] = 1
```

### Step 7: Assign unknown = 0

```python
hdr['quatern_c'] = 0
```

### Step 8: Assign unknown = 0

```python
hdr['quatern_d'] = 0
```

### Step 9: Call assert_true()

```python
assert_true(np.allclose(hdr.get_qform_quaternion(), [0, 1, 0, 0]))
```

### Step 10: Assign unknown = value

```python
hdr['quatern_b'] = 1 + np.finfo(np.float32).eps
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hdr.get_qform_quaternion(), [0, 1, 0, 0])
```


## Complete Example

```python
# Workflow
hdr = Nifti1Header()
hdr['quatern_b'] = 0
hdr['quatern_c'] = 0
hdr['quatern_d'] = 0
assert_true(np.allclose(hdr.get_qform_quaternion(), [1.0, 0, 0, 0]))
hdr['quatern_b'] = 1
hdr['quatern_c'] = 0
hdr['quatern_d'] = 0
assert_true(np.allclose(hdr.get_qform_quaternion(), [0, 1, 0, 0]))
hdr['quatern_b'] = 1 + np.finfo(np.float32).eps
assert_array_almost_equal(hdr.get_qform_quaternion(), [0, 1, 0, 0])
```

## Next Steps


---

*Source: test_nifti1.py:502 | Complexity: Advanced | Last updated: 2026-05-18*