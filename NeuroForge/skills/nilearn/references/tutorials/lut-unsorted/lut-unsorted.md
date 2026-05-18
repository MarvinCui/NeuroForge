# How To: Lut Unsorted

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test lut with wrong order of regions.

LUT, region_ids, region_names should be properly sorted after fit.
Result of region_ids, region_names
should still match content of extracted signals.

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
# Fixtures: surf_mesh, polydata_labels, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean
```

## Step-by-Step Guide

### Step 1: 'Test lut with wrong order of regions.\n\n    LUT, region_ids, region_names should be properly sorted after fit.\n    Result of region_ids, region_names\n    should still match content of extracted signals.\n    '

```python
'Test lut with wrong order of regions.\n\n    LUT, region_ids, region_names should be properly sorted after fit.\n    Result of region_ids, region_names\n    should still match content of extracted signals.\n    '
```

**Verification:**
```python
assert list(masker.lut.columns) == list(masker.lut_.columns)
```

### Step 2: Assign surf_label_img = SurfaceImage(...)

```python
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
```

**Verification:**
```python
assert masker.labels_ == [0.0, 1.0, 2.0, 10.0, 20.0]
```

### Step 3: Assign lut = pd.DataFrame(...)

```python
lut = pd.DataFrame(columns=['index', 'name'], data=[[1.0, 'one'], [20.0, 'twenty'], [10.0, 'ten'], [2.0, 'two']])
```

**Verification:**
```python
assert masker.lut_['name'].to_list() == ['Background', 'one', 'two', 'ten', 'twenty']
```

### Step 4: Assign masker = SurfaceLabelsMasker(...)

```python
masker = SurfaceLabelsMasker(labels_img=surf_label_img, lut=lut, standardize=None)
```

**Verification:**
```python
assert masker.region_names_ == {0: 'one', 1: 'two', 2: 'ten', 3: 'twenty'}
```

### Step 5: Assign masker = masker.fit(...)

```python
masker = masker.fit()
```

**Verification:**
```python
assert masker.region_ids_ == {'background': 0, 0: 1.0, 1: 2.0, 2: 10.0, 3: 20.0}
```

### Step 6: Assign data = value

```python
data = {'left': data_left_1d_with_expected_mean, 'right': data_right_1d_with_expected_mean}
```

**Verification:**
```python
assert isinstance(signal, np.ndarray)
```

### Step 7: Assign surf_img_1d = SurfaceImage(...)

```python
surf_img_1d = SurfaceImage(surf_mesh, data)
```

**Verification:**
```python
assert_array_equal(signal, np.asarray(expected_signal))
```

### Step 8: Assign signal = masker.transform(...)

```python
signal = masker.transform(surf_img_1d)
```

**Verification:**
```python
assert isinstance(signal, np.ndarray)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(signal, np.asarray(expected_signal))
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, polydata_labels, expected_signal, data_left_1d_with_expected_mean, data_right_1d_with_expected_mean

# Workflow
'Test lut with wrong order of regions.\n\n    LUT, region_ids, region_names should be properly sorted after fit.\n    Result of region_ids, region_names\n    should still match content of extracted signals.\n    '
surf_label_img = SurfaceImage(surf_mesh, polydata_labels)
lut = pd.DataFrame(columns=['index', 'name'], data=[[1.0, 'one'], [20.0, 'twenty'], [10.0, 'ten'], [2.0, 'two']])
masker = SurfaceLabelsMasker(labels_img=surf_label_img, lut=lut, standardize=None)
masker = masker.fit()
assert list(masker.lut.columns) == list(masker.lut_.columns)
assert masker.labels_ == [0.0, 1.0, 2.0, 10.0, 20.0]
assert masker.lut_['name'].to_list() == ['Background', 'one', 'two', 'ten', 'twenty']
assert masker.region_names_ == {0: 'one', 1: 'two', 2: 'ten', 3: 'twenty'}
assert masker.region_ids_ == {'background': 0, 0: 1.0, 1: 2.0, 2: 10.0, 3: 20.0}
data = {'left': data_left_1d_with_expected_mean, 'right': data_right_1d_with_expected_mean}
surf_img_1d = SurfaceImage(surf_mesh, data)
signal = masker.transform(surf_img_1d)
assert isinstance(signal, np.ndarray)
assert_array_equal(signal, np.asarray(expected_signal))
```

## Next Steps


---

*Source: test_surface_labels_masker.py:511 | Complexity: Advanced | Last updated: 2026-05-18*