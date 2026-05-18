# How To: Nifti Labels Masker Reduction Strategies

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests NiftiLabelsMasker strategies.

1. whether the usage of different reduction strategies work.
2. whether unrecognized strategies raise a ValueError
3. whether the default option is backwards compatible (calls "mean")

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
# Fixtures: affine_eye, strategy, function
```

## Step-by-Step Guide

### Step 1: 'Tests NiftiLabelsMasker strategies.\n\n    1. whether the usage of different reduction strategies work.\n    2. whether unrecognized strategies raise a ValueError\n    3. whether the default option is backwards compatible (calls "mean")\n    '

```python
'Tests NiftiLabelsMasker strategies.\n\n    1. whether the usage of different reduction strategies work.\n    2. whether unrecognized strategies raise a ValueError\n    3. whether the default option is backwards compatible (calls "mean")\n    '
```

**Verification:**
```python
assert result == expected_result
```

### Step 2: Assign test_values = value

```python
test_values = [-2.0, -1.0, 0.0, 1.0, 2]
```

**Verification:**
```python
assert default_masker.strategy == 'mean'
```

### Step 3: Assign img_data = np.array(...)

```python
img_data = np.array([[test_values, test_values]])
```

### Step 4: Assign labels_data = np.array(...)

```python
labels_data = np.array([[[0, 0, 0, 0, 0], [1, 1, 1, 1, 1]]], dtype=np.int8)
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(img_data, affine_eye)
```

### Step 6: Assign labels = Nifti1Image(...)

```python
labels = Nifti1Image(labels_data, affine_eye)
```

### Step 7: Assign expected_result = function(...)

```python
expected_result = function(test_values)
```

### Step 8: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(labels, strategy=strategy, standardize=None)
```

### Step 9: Assign result = masker.fit_transform.squeeze(...)

```python
result = masker.fit_transform([img]).squeeze()
```

**Verification:**
```python
assert result == expected_result
```

### Step 10: Assign default_masker = NiftiLabelsMasker(...)

```python
default_masker = NiftiLabelsMasker(labels, standardize=None)
```

**Verification:**
```python
assert default_masker.strategy == 'mean'
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, strategy, function

# Workflow
'Tests NiftiLabelsMasker strategies.\n\n    1. whether the usage of different reduction strategies work.\n    2. whether unrecognized strategies raise a ValueError\n    3. whether the default option is backwards compatible (calls "mean")\n    '
test_values = [-2.0, -1.0, 0.0, 1.0, 2]
img_data = np.array([[test_values, test_values]])
labels_data = np.array([[[0, 0, 0, 0, 0], [1, 1, 1, 1, 1]]], dtype=np.int8)
img = Nifti1Image(img_data, affine_eye)
labels = Nifti1Image(labels_data, affine_eye)
expected_result = function(test_values)
masker = NiftiLabelsMasker(labels, strategy=strategy, standardize=None)
result = masker.fit_transform([img]).squeeze()
assert result == expected_result
default_masker = NiftiLabelsMasker(labels, standardize=None)
assert default_masker.strategy == 'mean'
```

## Next Steps


---

*Source: test_nifti_labels_masker.py:251 | Complexity: Advanced | Last updated: 2026-05-18*