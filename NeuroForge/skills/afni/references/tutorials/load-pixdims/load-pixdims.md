# How To: Load Pixdims

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load pixdims

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
assert_array_equal(hdr.get_qform(), qaff)
```

### Step 2: Assign qaff = np.diag(...)

```python
qaff = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_array_equal(hdr.get_sform(), saff)
```

### Step 3: Assign saff = np.diag(...)

```python
saff = np.diag([5, 6, 7, 1])
```

**Verification:**
```python
assert_array_equal(img_hdr.get_qform(), qaff)
```

### Step 4: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert_array_equal(img_hdr.get_sform(), saff)
```

### Step 5: Call hdr.set_qform()

```python
hdr.set_qform(qaff)
```

**Verification:**
```python
assert_array_equal(img_hdr.get_zooms(), [2, 3, 4])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(hdr.get_qform(), qaff)
```

**Verification:**
```python
assert_array_equal(re_simg.get_data(), arr)
```

### Step 7: Call hdr.set_sform()

```python
hdr.set_sform(saff)
```

**Verification:**
```python
assert_array_equal(rimg_hdr.get_qform(), qaff)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(hdr.get_sform(), saff)
```

**Verification:**
```python
assert_array_equal(rimg_hdr.get_sform(), saff)
```

### Step 9: Assign simg = Nifti1Image(...)

```python
simg = Nifti1Image(arr, None, hdr)
```

**Verification:**
```python
assert_array_equal(rimg_hdr.get_zooms(), [2, 3, 4])
```

### Step 10: Assign img_hdr = simg.get_header(...)

```python
img_hdr = simg.get_header()
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(img_hdr.get_qform(), qaff)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(img_hdr.get_sform(), saff)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(img_hdr.get_zooms(), [2, 3, 4])
```

### Step 14: Assign fm = Nifti1Image.make_file_map(...)

```python
fm = Nifti1Image.make_file_map()
```

### Step 15: Assign unknown.fileobj = BytesIO(...)

```python
fm['image'].fileobj = BytesIO()
```

### Step 16: Call simg.to_file_map()

```python
simg.to_file_map(fm)
```

### Step 17: Assign re_simg = Nifti1Image.from_file_map(...)

```python
re_simg = Nifti1Image.from_file_map(fm)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(re_simg.get_data(), arr)
```

### Step 19: Assign rimg_hdr = re_simg.get_header(...)

```python
rimg_hdr = re_simg.get_header()
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(rimg_hdr.get_qform(), qaff)
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(rimg_hdr.get_sform(), saff)
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(rimg_hdr.get_zooms(), [2, 3, 4])
```


## Complete Example

```python
# Workflow
arr = np.arange(24).reshape((2, 3, 4))
qaff = np.diag([2, 3, 4, 1])
saff = np.diag([5, 6, 7, 1])
hdr = Nifti1Header()
hdr.set_qform(qaff)
assert_array_equal(hdr.get_qform(), qaff)
hdr.set_sform(saff)
assert_array_equal(hdr.get_sform(), saff)
simg = Nifti1Image(arr, None, hdr)
img_hdr = simg.get_header()
assert_array_equal(img_hdr.get_qform(), qaff)
assert_array_equal(img_hdr.get_sform(), saff)
assert_array_equal(img_hdr.get_zooms(), [2, 3, 4])
fm = Nifti1Image.make_file_map()
fm['image'].fileobj = BytesIO()
simg.to_file_map(fm)
re_simg = Nifti1Image.from_file_map(fm)
assert_array_equal(re_simg.get_data(), arr)
rimg_hdr = re_simg.get_header()
assert_array_equal(rimg_hdr.get_qform(), qaff)
assert_array_equal(rimg_hdr.get_sform(), saff)
assert_array_equal(rimg_hdr.get_zooms(), [2, 3, 4])
```

## Next Steps


---

*Source: test_nifti1.py:892 | Complexity: Advanced | Last updated: 2026-05-18*