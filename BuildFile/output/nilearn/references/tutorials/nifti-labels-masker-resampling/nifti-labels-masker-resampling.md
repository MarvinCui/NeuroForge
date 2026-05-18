# How To: Nifti Labels Masker Resampling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test to return resampled labels having number of labels        equal with transformed shape of 2nd dimension.

See https://github.com/nilearn/nilearn/issues/1673

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
# Fixtures: affine_eye, shape_3d_default, resampling_target, length, img_labels
```

## Step-by-Step Guide

### Step 1: 'Test to return resampled labels having number of labels        equal with transformed shape of 2nd dimension.\n\n    See https://github.com/nilearn/nilearn/issues/1673\n    '

```python
'Test to return resampled labels having number of labels        equal with transformed shape of 2nd dimension.\n\n    See https://github.com/nilearn/nilearn/issues/1673\n    '
```

**Verification:**
```python
assert n_resampled_labels - 1 == signals.shape[1]
```

### Step 2: Assign shape = value

```python
shape = (*shape_3d_default, length)
```

**Verification:**
```python
assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

### Step 3: Assign affine = value

```python
affine = 2 * affine_eye
```

### Step 4: Assign unknown = generate_random_img(...)

```python
fmri_img, _ = generate_random_img(shape, affine=affine)
```

### Step 5: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(labels_img=img_labels, resampling_target=resampling_target, standardize=None)
```

### Step 6: Assign resampled_labels_img = value

```python
resampled_labels_img = masker.labels_img_
```

### Step 7: Assign n_resampled_labels = len(...)

```python
n_resampled_labels = len(np.unique(get_data(resampled_labels_img)))
```

**Verification:**
```python
assert n_resampled_labels - 1 == signals.shape[1]
```

### Step 8: Assign compressed_img = masker.inverse_transform(...)

```python
compressed_img = masker.inverse_transform(signals)
```

### Step 9: Assign signals2 = masker.fit_transform(...)

```python
signals2 = masker.fit_transform(fmri_img)
```

### Step 10: Assign compressed_img2 = masker.inverse_transform(...)

```python
compressed_img2 = masker.inverse_transform(signals2)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

### Step 12: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

### Step 13: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, shape_3d_default, resampling_target, length, img_labels

# Workflow
'Test to return resampled labels having number of labels        equal with transformed shape of 2nd dimension.\n\n    See https://github.com/nilearn/nilearn/issues/1673\n    '
shape = (*shape_3d_default, length)
affine = 2 * affine_eye
fmri_img, _ = generate_random_img(shape, affine=affine)
masker = NiftiLabelsMasker(labels_img=img_labels, resampling_target=resampling_target, standardize=None)
if resampling_target == 'data':
    with pytest.warns(UserWarning, match='After resampling the label image to the data image, the following labels were removed'):
        signals = masker.fit_transform(fmri_img)
else:
    signals = masker.fit_transform(fmri_img)
resampled_labels_img = masker.labels_img_
n_resampled_labels = len(np.unique(get_data(resampled_labels_img)))
assert n_resampled_labels - 1 == signals.shape[1]
compressed_img = masker.inverse_transform(signals)
signals2 = masker.fit_transform(fmri_img)
compressed_img2 = masker.inverse_transform(signals2)
assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:346 | Complexity: Advanced | Last updated: 2026-05-18*