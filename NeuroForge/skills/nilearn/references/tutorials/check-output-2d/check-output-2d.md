# How To: Check Output 2D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check actual content of the transform and inverse_transform when
we have multiple timepoints.

- Use a label mask with more than one label.
- Use data with known content and expected mean.
  and background label data has random value.
- Check that output data is properly averaged,
  even when labels are spread across hemispheres.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.maskers`
- `nilearn.maskers.tests.conftest`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_mesh, polydata_labels, expected_mean_value, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean
```

## Step-by-Step Guide

### Step 1: 'Check actual content of the transform and inverse_transform when\n    we have multiple timepoints.\n\n    - Use a label mask with more than one label.\n    - Use data with known content and expected mean.\n      and background label data has random value.\n    - Check that output data is properly averaged,\n      even when labels are spread across hemispheres.\n    '

```python
'Check actual content of the transform and inverse_transform when\n    we have multiple timepoints.\n\n    - Use a label mask with more than one label.\n    - Use data with known content and expected mean.\n      and background label data has random value.\n    - Check that output data is properly averaged,\n      even when labels are spread across hemispheres.\n    '
```

**Verification:**
```python
assert signal.shape == (surf_img_2d.shape[1], masker.n_elements_)
```

### Step 2: Assign surf_label_img = SurfaceImage(...)

```python
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
```

**Verification:**
```python
assert_array_equal(signal, expected_signal)
```

### Step 3: Assign masker = SurfaceLabelsMasker(...)

```python
masker = SurfaceLabelsMasker(labels_img=surf_label_img, standardize=None)
```

**Verification:**
```python
assert masker.labels_ == [0, 1, 2, 10, 20]
```

### Step 4: Assign masker = masker.fit(...)

```python
masker = masker.fit()
```

**Verification:**
```python
assert masker.lut_['name'].to_list() == ['Background', '1', '2', '10', '20']
```

### Step 5: Assign data = value

```python
data = {'left': np.asarray([data_left_1d_with_expected_mean - 1, data_left_1d_with_expected_mean + 1]).T, 'right': np.asarray([data_right_1d_with_expected_mean - 1, data_right_1d_with_expected_mean + 1]).T}
```

**Verification:**
```python
assert masker.region_names_ == {0: '1', 1: '2', 2: '10', 3: '20'}
```

### Step 6: Assign surf_img_2d = SurfaceImage(...)

```python
surf_img_2d = SurfaceImage(surf_mesh, data)
```

**Verification:**
```python
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2, 2: 10, 3: 20}
```

### Step 7: Assign signal = masker.transform(...)

```python
signal = masker.transform(surf_img_2d)
```

**Verification:**
```python
assert img.shape[0] == surf_img_2d.shape[0]
```

### Step 8: Assign expected_signal = np.asarray(...)

```python
expected_signal = np.asarray([expected_signal - 1, expected_signal + 1])
```

**Verification:**
```python
assert_array_equal(img.data.parts['left'], expected_inverse_data['left'])
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(signal, expected_signal)
```

**Verification:**
```python
assert_array_equal(img.data.parts['right'], expected_inverse_data['right'])
```

### Step 10: Assign img = masker.inverse_transform(...)

```python
img = masker.inverse_transform(signal)
```

**Verification:**
```python
assert img.shape[0] == surf_img_2d.shape[0]
```

### Step 11: Assign expected_inverse_data = value

```python
expected_inverse_data = {'left': np.asarray([[expected_mean_value['2'] - 1, 0.0, expected_mean_value['10'] - 1, expected_mean_value['1'] - 1], [expected_mean_value['2'] + 1, 0.0, expected_mean_value['10'] + 1, expected_mean_value['1'] + 1]]).T, 'right': np.asarray([[expected_mean_value['10'] - 1, expected_mean_value['1'] - 1, expected_mean_value['20'] - 1, expected_mean_value['20'] - 1, 0.0], [expected_mean_value['10'] + 1, expected_mean_value['1'] + 1, expected_mean_value['20'] + 1, expected_mean_value['20'] + 1, 0.0]]).T}
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(img.data.parts['left'], expected_inverse_data['left'])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(img.data.parts['right'], expected_inverse_data['right'])
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, polydata_labels, expected_mean_value, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean

# Workflow
'Check actual content of the transform and inverse_transform when\n    we have multiple timepoints.\n\n    - Use a label mask with more than one label.\n    - Use data with known content and expected mean.\n      and background label data has random value.\n    - Check that output data is properly averaged,\n      even when labels are spread across hemispheres.\n    '
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
masker = SurfaceLabelsMasker(labels_img=surf_label_img, standardize=None)
masker = masker.fit()
data = {'left': np.asarray([data_left_1d_with_expected_mean - 1, data_left_1d_with_expected_mean + 1]).T, 'right': np.asarray([data_right_1d_with_expected_mean - 1, data_right_1d_with_expected_mean + 1]).T}
surf_img_2d = SurfaceImage(surf_mesh, data)
signal = masker.transform(surf_img_2d)
assert signal.shape == (surf_img_2d.shape[1], masker.n_elements_)
expected_signal = np.asarray([expected_signal - 1, expected_signal + 1])
assert_array_equal(signal, expected_signal)
assert masker.labels_ == [0, 1, 2, 10, 20]
assert masker.lut_['name'].to_list() == ['Background', '1', '2', '10', '20']
assert masker.region_names_ == {0: '1', 1: '2', 2: '10', 3: '20'}
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2, 2: 10, 3: 20}
img = masker.inverse_transform(signal)
assert img.shape[0] == surf_img_2d.shape[0]
expected_inverse_data = {'left': np.asarray([[expected_mean_value['2'] - 1, 0.0, expected_mean_value['10'] - 1, expected_mean_value['1'] - 1], [expected_mean_value['2'] + 1, 0.0, expected_mean_value['10'] + 1, expected_mean_value['1'] + 1]]).T, 'right': np.asarray([[expected_mean_value['10'] - 1, expected_mean_value['1'] - 1, expected_mean_value['20'] - 1, expected_mean_value['20'] - 1, 0.0], [expected_mean_value['10'] + 1, expected_mean_value['1'] + 1, expected_mean_value['20'] + 1, expected_mean_value['20'] + 1, 0.0]]).T}
assert_array_equal(img.data.parts['left'], expected_inverse_data['left'])
assert_array_equal(img.data.parts['right'], expected_inverse_data['right'])
```

## Next Steps


---

*Source: test_surface_labels_masker.py:565 | Complexity: Advanced | Last updated: 2026-05-18*