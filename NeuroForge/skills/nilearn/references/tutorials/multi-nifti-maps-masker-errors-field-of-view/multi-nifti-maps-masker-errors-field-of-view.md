# How To: Multi Nifti Maps Masker Errors Field Of View

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test all kinds of mismatches between shapes and between affines.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: tmp_path, affine_eye, length, create_files, shape_3d_default, img_maps
```

## Step-by-Step Guide

### Step 1: 'Test all kinds of mismatches between shapes and between affines.'

```python
'Test all kinds of mismatches between shapes and between affines.'
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

### Step 7: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask21_img, resampling_target=None, standardize=None)
```

### Step 8: Assign images = write_imgs_to_path(...)

```python
images = write_imgs_to_path(img_maps, mask12_img, file_path=tmp_path, create_files=create_files)
```

### Step 9: Assign unknown = images

```python
labels11, mask12 = images
```

### Step 10: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(labels11, resampling_target=None, standardize=None)
```

### Step 11: Call masker.fit()

```python
masker.fit()
```

### Step 12: Assign masker = MultiNiftiMapsMasker(...)

```python
masker = MultiNiftiMapsMasker(labels11, mask_img=mask12, resampling_target=None)
```

### Step 13: Call masker.fit()

```python
masker.fit()
```

### Step 14: Call masker.transform()

```python
masker.transform(fmri12_img)
```

### Step 15: Call masker.transform()

```python
masker.transform(fmri21_img)
```

### Step 16: Call masker.fit()

```python
masker.fit()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, affine_eye, length, create_files, shape_3d_default, img_maps

# Workflow
'Test all kinds of mismatches between shapes and between affines.'
shape2 = (12, 10, 14)
affine2 = np.diag((1, 2, 3, 1))
fmri12_img, mask12_img = generate_fake_fmri(shape_3d_default, affine=affine2, length=length)
fmri21_img, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
error_msg = 'Following field of view errors were detected'
masker = MultiNiftiMapsMasker(img_maps, mask_img=mask21_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match=error_msg):
    masker.fit()
images = write_imgs_to_path(img_maps, mask12_img, file_path=tmp_path, create_files=create_files)
labels11, mask12 = images
masker = MultiNiftiMapsMasker(labels11, resampling_target=None, standardize=None)
masker.fit()
with pytest.raises(ValueError, match=error_msg):
    masker.transform(fmri12_img)
with pytest.raises(ValueError, match=error_msg):
    masker.transform(fmri21_img)
masker = MultiNiftiMapsMasker(labels11, mask_img=mask12, resampling_target=None)
with pytest.raises(ValueError, match=error_msg):
    masker.fit()
```

## Next Steps


---

*Source: test_multi_nifti_maps_masker.py:179 | Complexity: Advanced | Last updated: 2026-05-18*