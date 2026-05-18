# How To: Crop Img To

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test crop img to

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign data = np.zeros(...)

```python
data = np.zeros((5, 6, 7))
```

**Verification:**
```python
assert (get_data(cropped_img) == 1).all()
```

### Step 2: Assign unknown = 1

```python
data[2:4, 1:5, 3:6] = 1
```

**Verification:**
```python
assert cropped_img.shape == (2, 4, 3)
```

### Step 3: Assign affine = np.diag(...)

```python
affine = np.diag((4, 3, 2, 1))
```

**Verification:**
```python
assert (cropped_img.affine[:3, 3] == new_origin).all()
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine=affine)
```

**Verification:**
```python
assert (get_data(cropped_img) == 2).all()
```

### Step 5: Assign slices = value

```python
slices = [slice(2, 4), slice(1, 5), slice(3, 6)]
```

**Verification:**
```python
assert (get_data(copied_cropped_img) == 2).all()
```

### Step 6: Assign cropped_img = _crop_img_to(...)

```python
cropped_img = _crop_img_to(img, slices, copy=False)
```

### Step 7: Assign new_origin = value

```python
new_origin = np.array((4, 3, 2)) * np.array((2, 1, 3))
```

**Verification:**
```python
assert (get_data(cropped_img) == 1).all()
```

### Step 8: Assign unknown = 2

```python
data[2:4, 1:5, 3:6] = 2
```

**Verification:**
```python
assert (get_data(cropped_img) == 2).all()
```

### Step 9: Assign copied_cropped_img = _crop_img_to(...)

```python
copied_cropped_img = _crop_img_to(img, slices)
```

### Step 10: Assign unknown = 1

```python
data[2:4, 1:5, 3:6] = 1
```

**Verification:**
```python
assert (get_data(copied_cropped_img) == 2).all()
```


## Complete Example

```python
# Workflow
data = np.zeros((5, 6, 7))
data[2:4, 1:5, 3:6] = 1
affine = np.diag((4, 3, 2, 1))
img = Nifti1Image(data, affine=affine)
slices = [slice(2, 4), slice(1, 5), slice(3, 6)]
cropped_img = _crop_img_to(img, slices, copy=False)
new_origin = np.array((4, 3, 2)) * np.array((2, 1, 3))
assert (get_data(cropped_img) == 1).all()
assert cropped_img.shape == (2, 4, 3)
assert (cropped_img.affine[:3, 3] == new_origin).all()
data[2:4, 1:5, 3:6] = 2
assert (get_data(cropped_img) == 2).all()
copied_cropped_img = _crop_img_to(img, slices)
data[2:4, 1:5, 3:6] = 1
assert (get_data(copied_cropped_img) == 2).all()
```

## Next Steps


---

*Source: test_image.py:519 | Complexity: Advanced | Last updated: 2026-05-18*