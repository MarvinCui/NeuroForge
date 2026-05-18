# How To: Multi Nifti Labels Masker Resampling Target

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test labels masker with resampling target in 'data', 'labels'.

Must return resampled labels having number of labels
equal with transformed shape of 2nd dimension.

This tests are added based on issue #1673 in Nilearn.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: "Test labels masker with resampling target in 'data', 'labels'.\n\n    Must return resampled labels having number of labels\n    equal with transformed shape of 2nd dimension.\n\n    This tests are added based on issue #1673 in Nilearn.\n    "

```python
"Test labels masker with resampling target in 'data', 'labels'.\n\n    Must return resampled labels having number of labels\n    equal with transformed shape of 2nd dimension.\n\n    This tests are added based on issue #1673 in Nilearn.\n    "
```

**Verification:**
```python
assert n_resampled_labels - 1 == signals.shape[1]
```

### Step 2: Assign shape = value

```python
shape = (13, 11, 12)
```

**Verification:**
```python
assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

### Step 3: Assign affine = value

```python
affine = np.eye(4) * 2
```

### Step 4: Assign unknown = generate_fake_fmri(...)

```python
fmri_img, _ = generate_fake_fmri(shape, affine=affine, length=21)
```

### Step 5: Assign labels_img = generate_labeled_regions(...)

```python
labels_img = generate_labeled_regions((9, 8, 6), affine=np.eye(4), n_regions=10)
```

### Step 6: Assign masker = MultiNiftiLabelsMasker(...)

```python
masker = MultiNiftiLabelsMasker(labels_img=labels_img, resampling_target=resampling_target, keep_masked_labels=True, standardize=None)
```

### Step 7: Assign resampled_labels_img = value

```python
resampled_labels_img = masker.labels_img_
```

### Step 8: Assign n_resampled_labels = len(...)

```python
n_resampled_labels = len(np.unique(get_data(resampled_labels_img)))
```

**Verification:**
```python
assert n_resampled_labels - 1 == signals.shape[1]
```

### Step 9: Assign compressed_img = masker.inverse_transform(...)

```python
compressed_img = masker.inverse_transform(signals)
```

### Step 10: Assign compressed_img2 = masker.inverse_transform(...)

```python
compressed_img2 = masker.inverse_transform(signals2)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

### Step 12: Assign signals2 = masker.fit_transform(...)

```python
signals2 = masker.fit_transform(fmri_img)
```

### Step 13: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```

### Step 14: Assign signals = masker.fit_transform(...)

```python
signals = masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Workflow
"Test labels masker with resampling target in 'data', 'labels'.\n\n    Must return resampled labels having number of labels\n    equal with transformed shape of 2nd dimension.\n\n    This tests are added based on issue #1673 in Nilearn.\n    "
shape = (13, 11, 12)
affine = np.eye(4) * 2
fmri_img, _ = generate_fake_fmri(shape, affine=affine, length=21)
labels_img = generate_labeled_regions((9, 8, 6), affine=np.eye(4), n_regions=10)
for resampling_target in ['data', 'labels']:
    masker = MultiNiftiLabelsMasker(labels_img=labels_img, resampling_target=resampling_target, keep_masked_labels=True, standardize=None)
    if resampling_target == 'data':
        with pytest.warns(UserWarning, match='After resampling the label image to the data image, the following labels were removed'), pytest.warns(FutureWarning, match='In version 0.15.0, "keep_masked_labels" parameter will be removed'):
            signals = masker.fit_transform(fmri_img)
    else:
        with pytest.warns(FutureWarning, match='In version 0.15.0, "keep_masked_labels" parameter will be removed'):
            signals = masker.fit_transform(fmri_img)
    resampled_labels_img = masker.labels_img_
    n_resampled_labels = len(np.unique(get_data(resampled_labels_img)))
    assert n_resampled_labels - 1 == signals.shape[1]
    compressed_img = masker.inverse_transform(signals)
    with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
        signals2 = masker.fit_transform(fmri_img)
    compressed_img2 = masker.inverse_transform(signals2)
    assert_array_equal(get_data(compressed_img), get_data(compressed_img2))
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:381 | Complexity: Advanced | Last updated: 2026-05-18*