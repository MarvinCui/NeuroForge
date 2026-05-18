# How To: Multi Nifti Labels Masker Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test errors in MultiNiftiLabelsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: affine_eye, shape_3d_default, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Test errors in MultiNiftiLabelsMasker.'

```python
'Test errors in MultiNiftiLabelsMasker.'
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

### Step 6: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
```

### Step 7: Call masker11.fit()

```python
masker11.fit()
```

### Step 8: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask12_img, resampling_target=None)
```

### Step 9: Assign masker11 = MultiNiftiLabelsMasker(...)

```python
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask21_img, resampling_target=None)
```

### Step 10: Call masker11.transform()

```python
masker11.transform(fmri12_img)
```

### Step 11: Call masker11.transform()

```python
masker11.transform(fmri21_img)
```

### Step 12: Call masker11.fit()

```python
masker11.fit()
```

### Step 13: Call masker11.fit()

```python
masker11.fit()
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, length, img_labels

# Workflow
'Test errors in MultiNiftiLabelsMasker.'
shape2 = (12, 10, 14)
affine2 = np.diag((1, 2, 3, 1))
fmri12_img, mask12_img = generate_fake_fmri(shape_3d_default, affine=affine2, length=length)
fmri21_img, mask21_img = generate_fake_fmri(shape2, affine=affine_eye, length=length)
masker11 = MultiNiftiLabelsMasker(img_labels, resampling_target=None, standardize=None)
masker11.fit()
with pytest.raises(ValueError, match='Images have different affine matrices.'):
    masker11.transform(fmri12_img)
with pytest.raises(ValueError, match='Images have incompatible shapes.'):
    masker11.transform(fmri21_img)
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask12_img, resampling_target=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
masker11 = MultiNiftiLabelsMasker(img_labels, mask_img=mask21_img, resampling_target=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:137 | Complexity: Advanced | Last updated: 2026-05-18*