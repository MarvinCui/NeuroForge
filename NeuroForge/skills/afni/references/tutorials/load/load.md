# How To: Load

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load

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

### Step 1: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24).reshape((2, 3, 4))
```

**Verification:**
```python
assert_array_equal(arr, nifti1.load('test.nii').get_data())
```

### Step 2: Assign aff = np.diag(...)

```python
aff = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_array_equal(arr, nifti1.load('test.img').get_data())
```

### Step 3: Assign simg = Nifti1Image(...)

```python
simg = Nifti1Image(arr, aff)
```

**Verification:**
```python
assert_array_equal(arr, nifti1.load('test.hdr').get_data())
```

### Step 4: Assign pimg = Nifti1Pair(...)

```python
pimg = Nifti1Pair(arr, aff)
```

### Step 5: Call nifti1.save()

```python
nifti1.save(simg, 'test.nii')
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(arr, nifti1.load('test.nii').get_data())
```

### Step 7: Call nifti1.save()

```python
nifti1.save(simg, 'test.img')
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(arr, nifti1.load('test.img').get_data())
```

### Step 9: Call nifti1.save()

```python
nifti1.save(simg, 'test.hdr')
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(arr, nifti1.load('test.hdr').get_data())
```


## Complete Example

```python
# Workflow
arr = np.arange(24).reshape((2, 3, 4))
aff = np.diag([2, 3, 4, 1])
simg = Nifti1Image(arr, aff)
pimg = Nifti1Pair(arr, aff)
with InTemporaryDirectory():
    nifti1.save(simg, 'test.nii')
    assert_array_equal(arr, nifti1.load('test.nii').get_data())
    nifti1.save(simg, 'test.img')
    assert_array_equal(arr, nifti1.load('test.img').get_data())
    nifti1.save(simg, 'test.hdr')
    assert_array_equal(arr, nifti1.load('test.hdr').get_data())
```

## Next Steps


---

*Source: test_nifti1.py:876 | Complexity: Advanced | Last updated: 2026-05-18*