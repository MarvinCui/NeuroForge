# How To: Multi Nifti Labels Masker Reduction Strategies

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests strategies of MultiNiftiLabelsMasker.

- whether the usage of different reduction strategies work
- whether the default option is backwards compatible (calls "mean")

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
# Fixtures: affine_eye, test_values, strategy, fn
```

## Step-by-Step Guide

### Step 1: 'Tests strategies of MultiNiftiLabelsMasker.\n\n    - whether the usage of different reduction strategies work\n    - whether the default option is backwards compatible (calls "mean")\n    '

```python
'Tests strategies of MultiNiftiLabelsMasker.\n\n    - whether the usage of different reduction strategies work\n    - whether the default option is backwards compatible (calls "mean")\n    '
```

**Verification:**
```python
assert r.squeeze() == expected_result
```

### Step 2: Assign img_data = np.array(...)

```python
img_data = np.array([[test_values, test_values]])
```

**Verification:**
```python
assert default_masker.strategy == 'mean'
```

### Step 3: Assign labels_data = np.array(...)

```python
labels_data = np.array([[[0, 0, 0, 0, 0], [1, 1, 1, 1, 1]]], dtype=np.int8)
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(img_data, affine_eye)
```

### Step 5: Assign labels = Nifti1Image(...)

```python
labels = Nifti1Image(labels_data, affine_eye)
```

### Step 6: Assign masker = MultiNiftiLabelsMasker(...)

```python
masker = MultiNiftiLabelsMasker(labels, strategy=strategy, standardize=None)
```

### Step 7: Assign results = masker.fit_transform(...)

```python
results = masker.fit_transform([img, img])
```

### Step 8: Assign expected_result = fn(...)

```python
expected_result = fn(test_values)
```

### Step 9: Assign default_masker = MultiNiftiLabelsMasker(...)

```python
default_masker = MultiNiftiLabelsMasker(labels)
```

**Verification:**
```python
assert default_masker.strategy == 'mean'
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, test_values, strategy, fn

# Workflow
'Tests strategies of MultiNiftiLabelsMasker.\n\n    - whether the usage of different reduction strategies work\n    - whether the default option is backwards compatible (calls "mean")\n    '
img_data = np.array([[test_values, test_values]])
labels_data = np.array([[[0, 0, 0, 0, 0], [1, 1, 1, 1, 1]]], dtype=np.int8)
img = Nifti1Image(img_data, affine_eye)
labels = Nifti1Image(labels_data, affine_eye)
masker = MultiNiftiLabelsMasker(labels, strategy=strategy, standardize=None)
results = masker.fit_transform([img, img])
expected_result = fn(test_values)
for r in results:
    assert r.squeeze() == expected_result
default_masker = MultiNiftiLabelsMasker(labels)
assert default_masker.strategy == 'mean'
```

## Next Steps


---

*Source: test_multi_nifti_labels_masker.py:218 | Complexity: Advanced | Last updated: 2026-05-18*