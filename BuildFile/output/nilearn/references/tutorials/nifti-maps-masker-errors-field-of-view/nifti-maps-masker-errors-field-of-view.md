# How To: Nifti Maps Masker Errors Field Of View

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check field of view errors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: tmp_path, length, affine_eye, shape_3d_default, create_files, img_maps
```

## Step-by-Step Guide

### Step 1: 'Check field of view errors.'

```python
'Check field of view errors.'
```

### Step 2: Assign shape2 = value

```python
shape2 = (12, 10, 14)
```

### Step 3: Assign affine2 = np.diag(...)

```python
affine2 = np.diag((1, 2, 3, 1))
```

### Step 4: Assign unknown = generate_fake_fmri(...)

```python
fmri12_img, mask12_img = generate_fake_fmri(shape_3d_default, affine=affine2, length=length)
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
fmri21_img, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
```

### Step 6: Assign error_msg = 'Following field of view errors were detected'

```python
error_msg = 'Following field of view errors were detected'
```

### Step 7: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(img_maps, mask_img=mask21_img, resampling_target=None, standardize=None)
```

### Step 8: Assign images = write_imgs_to_path(...)

```python
images = write_imgs_to_path(img_maps, mask12_img, file_path=tmp_path, create_files=create_files)
```

### Step 9: Assign unknown = images

```python
labels11, mask12 = images
```

### Step 10: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(labels11, resampling_target=None, standardize=None)
```

### Step 11: Assign masker = NiftiMapsMasker(...)

```python
masker = NiftiMapsMasker(labels11, mask_img=mask12, resampling_target=None)
```

### Step 12: Call masker.fit()

```python
masker.fit()
```

### Step 13: Call masker.fit_transform()

```python
masker.fit_transform(fmri12_img)
```

### Step 14: Call masker.fit_transform()

```python
masker.fit_transform(fmri21_img)
```

### Step 15: Call masker.fit()

```python
masker.fit()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, length, affine_eye, shape_3d_default, create_files, img_maps

# Workflow
'Check field of view errors.'
shape2 = (12, 10, 14)
affine2 = np.diag((1, 2, 3, 1))
fmri12_img, mask12_img = generate_fake_fmri(shape_3d_default, affine=affine2, length=length)
fmri21_img, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
error_msg = 'Following field of view errors were detected'
masker = NiftiMapsMasker(img_maps, mask_img=mask21_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match=error_msg):
    masker.fit()
images = write_imgs_to_path(img_maps, mask12_img, file_path=tmp_path, create_files=create_files)
labels11, mask12 = images
masker = NiftiMapsMasker(labels11, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match=error_msg):
    masker.fit_transform(fmri12_img)
with pytest.raises(ValueError, match=error_msg):
    masker.fit_transform(fmri21_img)
masker = NiftiMapsMasker(labels11, mask_img=mask12, resampling_target=None)
with pytest.raises(ValueError, match=error_msg):
    masker.fit()
```

## Next Steps


---

*Source: test_nifti_maps_masker.py:132 | Complexity: Advanced | Last updated: 2026-05-18*