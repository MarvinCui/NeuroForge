# How To: Smooth Img

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Checks added functionalities compared to image._smooth_array().

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
# Fixtures: tmp_path, create_files
```

## Step-by-Step Guide

### Step 1: 'Checks added functionalities compared to image._smooth_array().'

```python
'Checks added functionalities compared to image._smooth_array().'
```

**Verification:**
```python
assert isinstance(out, list)
```

### Step 2: Assign shapes = value

```python
shapes = ((10, 11, 12), (13, 14, 15))
```

**Verification:**
```python
assert len(out) == 2
```

### Step 3: Assign lengths = value

```python
lengths = (17, 18)
```

**Verification:**
```python
assert o.shape == (*s, l)
```

### Step 4: Assign fwhm = value

```python
fwhm = (1.0, 2.0, 3.0)
```

**Verification:**
```python
assert isinstance(out, Nifti1Image)
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
img1, _ = generate_fake_fmri(shape=shapes[0], length=lengths[0])
```

**Verification:**
```python
assert out.shape == shapes[0] + (lengths[0],)
```

### Step 6: Assign unknown = generate_fake_fmri(...)

```python
img2, _ = generate_fake_fmri(shape=shapes[1], length=lengths[1])
```

### Step 7: Assign imgs = testing.write_imgs_to_path(...)

```python
imgs = testing.write_imgs_to_path(img1, img2, file_path=tmp_path, create_files=create_files)
```

### Step 8: Assign out = smooth_img(...)

```python
out = smooth_img(imgs, fwhm)
```

**Verification:**
```python
assert isinstance(out, list)
```

### Step 9: Assign out = smooth_img(...)

```python
out = smooth_img(imgs[0], fwhm)
```

**Verification:**
```python
assert isinstance(out, Nifti1Image)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, create_files

# Workflow
'Checks added functionalities compared to image._smooth_array().'
shapes = ((10, 11, 12), (13, 14, 15))
lengths = (17, 18)
fwhm = (1.0, 2.0, 3.0)
img1, _ = generate_fake_fmri(shape=shapes[0], length=lengths[0])
img2, _ = generate_fake_fmri(shape=shapes[1], length=lengths[1])
imgs = testing.write_imgs_to_path(img1, img2, file_path=tmp_path, create_files=create_files)
out = smooth_img(imgs, fwhm)
assert isinstance(out, list)
assert len(out) == 2
for o, s, l in zip(out, shapes, lengths, strict=False):
    assert o.shape == (*s, l)
out = smooth_img(imgs[0], fwhm)
assert isinstance(out, Nifti1Image)
assert out.shape == shapes[0] + (lengths[0],)
```

## Next Steps


---

*Source: test_image.py:359 | Complexity: Advanced | Last updated: 2026-05-18*