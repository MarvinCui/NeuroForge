# How To: Negative Load Save

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test negative load save

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `shutil`
- `tempfile`
- `py3k`
- `numpy`
- `tmpdirs`
- `volumeutils`
- `numpy.testing`
- `nose.tools`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (1, 2, 5)
```

**Verification:**
```python
assert_array_almost_equal(re_img.get_data(), data, 4)
```

### Step 2: Assign data = value

```python
data = np.arange(10).reshape(shape) - 10.0
```

### Step 3: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 4: Assign hdr = ni1.Nifti1Header(...)

```python
hdr = ni1.Nifti1Header()
```

### Step 5: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int16)
```

### Step 6: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine, hdr)
```

### Step 7: Assign str_io = BytesIO(...)

```python
str_io = BytesIO()
```

### Step 8: Assign unknown.fileobj = str_io

```python
img.file_map['image'].fileobj = str_io
```

### Step 9: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 10: Call str_io.seek()

```python
str_io.seek(0)
```

### Step 11: Assign re_img = Nifti1Image.from_file_map(...)

```python
re_img = Nifti1Image.from_file_map(img.file_map)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(re_img.get_data(), data, 4)
```


## Complete Example

```python
# Workflow
shape = (1, 2, 5)
data = np.arange(10).reshape(shape) - 10.0
affine = np.eye(4)
hdr = ni1.Nifti1Header()
hdr.set_data_dtype(np.int16)
img = Nifti1Image(data, affine, hdr)
str_io = BytesIO()
img.file_map['image'].fileobj = str_io
img.to_file_map()
str_io.seek(0)
re_img = Nifti1Image.from_file_map(img.file_map)
assert_array_almost_equal(re_img.get_data(), data, 4)
```

## Next Steps


---

*Source: test_image_load_save.py:202 | Complexity: Advanced | Last updated: 2026-05-18*