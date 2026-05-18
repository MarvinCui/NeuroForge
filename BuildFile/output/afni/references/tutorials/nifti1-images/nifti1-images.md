# How To: Nifti1 Images

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nifti1 images

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

### Step 1: Assign shape = value

```python
shape = (2, 4, 6)
```

**Verification:**
```python
assert_equal(img.shape, shape)
```

### Step 2: Assign npt = value

```python
npt = np.float32
```

**Verification:**
```python
assert_array_equal(img2.get_data(), data)
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
```

**Verification:**
```python
assert_true(isinstance(img3, img.__class__))
```

### Step 4: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

**Verification:**
```python
assert_array_equal(img3.get_data(), data)
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

**Verification:**
```python
assert_equal(img3.get_header(), img.get_header())
```

### Step 6: Call assert_equal()

```python
assert_equal(img.shape, shape)
```

### Step 7: Call img.set_data_dtype()

```python
img.set_data_dtype(npt)
```

### Step 8: Assign stio = BytesIO(...)

```python
stio = BytesIO()
```

### Step 9: Assign unknown.fileobj = stio

```python
img.file_map['image'].fileobj = stio
```

### Step 10: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 11: Assign img2 = Nifti1Image.from_file_map(...)

```python
img2 = Nifti1Image.from_file_map(img.file_map)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(img2.get_data(), data)
```

### Step 13: Assign fname = os.path.join(...)

```python
fname = os.path.join(tmpdir, 'test.nii' + ext)
```

### Step 14: Call img.to_filename()

```python
img.to_filename(fname)
```

### Step 15: Assign img3 = Nifti1Image.load(...)

```python
img3 = Nifti1Image.load(fname)
```

### Step 16: Call assert_true()

```python
assert_true(isinstance(img3, img.__class__))
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(img3.get_data(), data)
```

### Step 18: Call assert_equal()

```python
assert_equal(img3.get_header(), img.get_header())
```


## Complete Example

```python
# Workflow
shape = (2, 4, 6)
npt = np.float32
data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
affine = np.diag([1, 2, 3, 1])
img = Nifti1Image(data, affine)
assert_equal(img.shape, shape)
img.set_data_dtype(npt)
stio = BytesIO()
img.file_map['image'].fileobj = stio
img.to_file_map()
img2 = Nifti1Image.from_file_map(img.file_map)
assert_array_equal(img2.get_data(), data)
with InTemporaryDirectory() as tmpdir:
    for ext in ('.gz', '.bz2'):
        fname = os.path.join(tmpdir, 'test.nii' + ext)
        img.to_filename(fname)
        img3 = Nifti1Image.load(fname)
        assert_true(isinstance(img3, img.__class__))
        assert_array_equal(img3.get_data(), data)
        assert_equal(img3.get_header(), img.get_header())
        del img3
```

## Next Steps


---

*Source: test_nifti1.py:704 | Complexity: Advanced | Last updated: 2026-05-18*