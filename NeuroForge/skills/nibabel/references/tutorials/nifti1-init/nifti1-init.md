# How To: Nifti1 Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nifti1 init

## Prerequisites

**Required Modules:**
- `contextlib`
- `gzip`
- `pickle`
- `io`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `packaging.version`
- `arrayproxy`
- `deprecator`
- `nifti1`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`
- `test_openers`


## Step-by-Step Guide

### Step 1: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert ap.file_like == bio
```

### Step 2: Assign shape = value

```python
shape = (2, 3, 4)
```

**Verification:**
```python
assert ap.shape == shape
```

### Step 3: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
```

### Step 4: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24, dtype=np.int16).reshape(shape)
```

**Verification:**
```python
assert ap.file_like == 'test.nii'
```

### Step 5: Call write_raw_data()

```python
write_raw_data(arr, hdr, bio)
```

**Verification:**
```python
assert ap.shape == shape
```

### Step 6: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(2, 10)
```

**Verification:**
```python
assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
```

### Step 7: Assign ap = ArrayProxy(...)

```python
ap = ArrayProxy(bio, hdr)
```

**Verification:**
```python
assert ap.file_like == bio
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
```

### Step 9: Assign f = open(...)

```python
f = open('test.nii', 'wb')
```

### Step 10: Call write_raw_data()

```python
write_raw_data(arr, hdr, f)
```

### Step 11: Call f.close()

```python
f.close()
```

### Step 12: Assign ap = ArrayProxy(...)

```python
ap = ArrayProxy('test.nii', hdr)
```

**Verification:**
```python
assert ap.file_like == 'test.nii'
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
```


## Complete Example

```python
# Workflow
bio = BytesIO()
shape = (2, 3, 4)
hdr = Nifti1Header()
arr = np.arange(24, dtype=np.int16).reshape(shape)
write_raw_data(arr, hdr, bio)
hdr.set_slope_inter(2, 10)
ap = ArrayProxy(bio, hdr)
assert ap.file_like == bio
assert ap.shape == shape
assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
with InTemporaryDirectory():
    f = open('test.nii', 'wb')
    write_raw_data(arr, hdr, f)
    f.close()
    ap = ArrayProxy('test.nii', hdr)
    assert ap.file_like == 'test.nii'
    assert ap.shape == shape
    assert_array_equal(np.asarray(ap), arr * 2.0 + 10)
```

## Next Steps


---

*Source: test_arrayproxy.py:138 | Complexity: Advanced | Last updated: 2026-05-18*