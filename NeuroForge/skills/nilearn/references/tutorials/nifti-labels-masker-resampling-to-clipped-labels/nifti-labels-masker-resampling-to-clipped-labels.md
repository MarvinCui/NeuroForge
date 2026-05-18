# How To: Nifti Labels Masker Resampling To Clipped Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test with clipped labels.

Mask does not contain all labels.

Shapes do matter in that case,
because there is some resampling taking place.

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

### Step 1: 'Test with clipped labels.\n\n    Mask does not contain all labels.\n\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '

```python
'Test with clipped labels.\n\n    Mask does not contain all labels.\n\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '
```

**Verification:**
```python
assert_almost_equal(masker.labels_img_.affine, labels33_img.affine)
```

### Step 2: Assign shape1 = value

```python
shape1 = (*shape_3d_default, length)
```

**Verification:**
```python
assert masker.labels_img_.shape == labels33_img.shape
```

### Step 3: Assign shape2 = value

```python
shape2 = (8, 9, 10, length)
```

**Verification:**
```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

### Step 4: Assign shape3 = value

```python
shape3 = (16, 18, 20)
```

**Verification:**
```python
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
```

### Step 5: Assign unknown = generate_random_img(...)

```python
fmri11_img, _ = generate_random_img(shape1, affine=affine_eye)
```

**Verification:**
```python
assert uniq_labels[0] == 0
```

### Step 6: Assign unknown = generate_random_img(...)

```python
_, mask22_img = generate_random_img(shape2, affine=affine_eye)
```

**Verification:**
```python
assert len(uniq_labels) - 1 == n_regions
```

### Step 7: Assign labels33_img = generate_labeled_regions(...)

```python
labels33_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
```

**Verification:**
```python
assert signals.shape == (length, n_regions)
```

### Step 8: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(labels33_img, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
```

**Verification:**
```python
assert (signals.var(axis=0) == 0).sum() < n_regions
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(masker.labels_img_.affine, labels33_img.affine)
```

**Verification:**
```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

### Step 11: Assign uniq_labels = np.unique(...)

```python
uniq_labels = np.unique(get_data(masker.labels_img_))
```

**Verification:**
```python
assert uniq_labels[0] == 0
```

### Step 12: Assign fmri11_img_r = masker.inverse_transform(...)

```python
fmri11_img_r = masker.inverse_transform(signals)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
```

**Verification:**
```python
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

### Step 14: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri11_img)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, n_regions, length

# Workflow
'Test with clipped labels.\n\n    Mask does not contain all labels.\n\n    Shapes do matter in that case,\n    because there is some resampling taking place.\n    '
shape1 = (*shape_3d_default, length)
shape2 = (8, 9, 10, length)
shape3 = (16, 18, 20)
fmri11_img, _ = generate_random_img(shape1, affine=affine_eye)
_, mask22_img = generate_random_img(shape2, affine=affine_eye)
labels33_img = generate_labeled_regions(shape3, n_regions, affine=affine_eye)
masker = NiftiLabelsMasker(labels33_img, mask_img=mask22_img, resampling_target='labels', keep_masked_labels=True, standardize=None)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    signals = masker.fit_transform(fmri11_img)
assert_almost_equal(masker.labels_img_.affine, labels33_img.affine)
assert masker.labels_img_.shape == labels33_img.shape
assert_almost_equal(masker.mask_img_.affine, masker.labels_img_.affine)
assert masker.mask_img_.shape == masker.labels_img_.shape[:3]
uniq_labels = np.unique(get_data(masker.labels_img_))
assert uniq_labels[0] == 0
assert len(uniq_labels) - 1 == n_regions
assert signals.shape == (length, n_regions)
assert (signals.var(axis=0) == 0).sum() < n_regions
fmri11_img_r = masker.inverse_transform(signals)
assert_almost_equal(fmri11_img_r.affine, masker.labels_img_.affine)
assert fmri11_img_r.shape == (*masker.labels_img_.shape[:3], length)
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:440 | Complexity: Advanced | Last updated: 2026-05-18*