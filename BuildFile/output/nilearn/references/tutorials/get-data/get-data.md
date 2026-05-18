# How To: Get Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `re`
- `warnings`
- `collections.abc`
- `pathlib`
- `joblib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`
- `nilearn.surface.surface`
- `nilearn.surface.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, shape_3d_default
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_fake_fmri(...)

```python
img, *_ = generate_fake_fmri(shape=shape_3d_default)
```

**Verification:**
```python
assert data.shape == img.shape
```

### Step 2: Assign data = get_data(...)

```python
data = get_data(img)
```

**Verification:**
```python
assert data is img._data_cache
```

### Step 3: Assign mask_img = new_img_like(...)

```python
mask_img = new_img_like(img, data > 0)
```

**Verification:**
```python
assert data.dtype == np.dtype('uint8')
```

### Step 4: Assign data = get_data(...)

```python
data = get_data(mask_img)
```

**Verification:**
```python
assert len(data.shape) == 3
```

### Step 5: Assign img_3d = index_img(...)

```python
img_3d = index_img(img, 0)
```

**Verification:**
```python
assert len(data.shape) == 4
```

### Step 6: Assign filename = str(...)

```python
filename = str(tmp_path / 'img_{}.nii.gz')
```

### Step 7: Call img_3d.to_filename()

```python
img_3d.to_filename(filename.format('a'))
```

### Step 8: Call img_3d.to_filename()

```python
img_3d.to_filename(filename.format('b'))
```

### Step 9: Assign data = get_data(...)

```python
data = get_data(filename.format('a'))
```

**Verification:**
```python
assert len(data.shape) == 3
```

### Step 10: Assign data = get_data(...)

```python
data = get_data(filename.format('*'))
```

**Verification:**
```python
assert len(data.shape) == 4
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, shape_3d_default

# Workflow
img, *_ = generate_fake_fmri(shape=shape_3d_default)
data = get_data(img)
assert data.shape == img.shape
assert data is img._data_cache
mask_img = new_img_like(img, data > 0)
data = get_data(mask_img)
assert data.dtype == np.dtype('uint8')
img_3d = index_img(img, 0)
filename = str(tmp_path / 'img_{}.nii.gz')
img_3d.to_filename(filename.format('a'))
img_3d.to_filename(filename.format('b'))
data = get_data(filename.format('a'))
assert len(data.shape) == 3
data = get_data(filename.format('*'))
assert len(data.shape) == 4
```

## Next Steps


---

*Source: test_image.py:184 | Complexity: Advanced | Last updated: 2026-05-18*