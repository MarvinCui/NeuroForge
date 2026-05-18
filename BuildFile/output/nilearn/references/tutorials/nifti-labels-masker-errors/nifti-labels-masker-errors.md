# How To: Nifti Labels Masker Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check working of shape/affine checks.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `numpy`
- `pandas`
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
# Fixtures: affine_eye, shape_3d_default, n_regions, length
```

## Step-by-Step Guide

### Step 1: 'Check working of shape/affine checks.'

```python
'Check working of shape/affine checks.'
```

### Step 2: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(standardize=None)
```

### Step 3: Assign shape1 = value

```python
shape1 = (*shape_3d_default, length)
```

### Step 4: Assign shape2 = value

```python
shape2 = (12, 10, 14, length)
```

### Step 5: Assign affine2 = np.diag(...)

```python
affine2 = np.diag((1, 2, 3, 1))
```

### Step 6: Assign unknown = generate_random_img(...)

```python
fmri12_img, mask12_img = generate_random_img(shape1, affine=affine2)
```

### Step 7: Assign unknown = generate_random_img(...)

```python
fmri21_img, mask21_img = generate_random_img(shape2, affine=affine_eye)
```

### Step 8: Assign labels11_img = generate_labeled_regions(...)

```python
labels11_img = generate_labeled_regions(shape1[:3], affine=affine_eye, n_regions=n_regions)
```

### Step 9: Assign masker11 = NiftiLabelsMasker(...)

```python
masker11 = NiftiLabelsMasker(labels11_img, resampling_target=None, standardize=None)
```

### Step 10: Call masker11.fit()

```python
masker11.fit()
```

### Step 11: Assign masker11 = NiftiLabelsMasker(...)

```python
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask12_img, resampling_target=None, standardize=None)
```

### Step 12: Assign masker11 = NiftiLabelsMasker(...)

```python
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask21_img, resampling_target=None, standardize=None)
```

### Step 13: Call masker.fit()

```python
masker.fit()
```

### Step 14: Call masker11.transform()

```python
masker11.transform(fmri12_img)
```

### Step 15: Call masker11.transform()

```python
masker11.transform(fmri21_img)
```

### Step 16: Call masker11.fit()

```python
masker11.fit()
```

### Step 17: Call masker11.fit()

```python
masker11.fit()
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, n_regions, length

# Workflow
'Check working of shape/affine checks.'
masker = NiftiLabelsMasker(standardize=None)
with pytest.raises(TypeError, match='input should be a NiftiLike object'):
    masker.fit()
shape1 = (*shape_3d_default, length)
shape2 = (12, 10, 14, length)
affine2 = np.diag((1, 2, 3, 1))
fmri12_img, mask12_img = generate_random_img(shape1, affine=affine2)
fmri21_img, mask21_img = generate_random_img(shape2, affine=affine_eye)
labels11_img = generate_labeled_regions(shape1[:3], affine=affine_eye, n_regions=n_regions)
masker11 = NiftiLabelsMasker(labels11_img, resampling_target=None, standardize=None)
masker11.fit()
with pytest.raises(ValueError, match='Images have different affine matrices.'):
    masker11.transform(fmri12_img)
with pytest.raises(ValueError, match='Images have incompatible shapes.'):
    masker11.transform(fmri21_img)
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask12_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
masker11 = NiftiLabelsMasker(labels11_img, mask_img=mask21_img, resampling_target=None, standardize=None)
with pytest.raises(ValueError, match='Following field of view errors were detected'):
    masker11.fit()
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:122 | Complexity: Advanced | Last updated: 2026-05-18*