# How To: Transform With Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test transform extract signals with a mask and check warning.

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
# Fixtures: surf_mesh, surf_img_2d
```

## Step-by-Step Guide

### Step 1: 'Test transform extract signals with a mask and check warning.'

```python
'Test transform extract signals with a mask and check warning.'
```

**Verification:**
```python
assert isinstance(signal, np.ndarray)
```

### Step 2: Assign labels_data = value

```python
labels_data = {'left': np.asarray([1, 1, 1, 2]), 'right': np.asarray([3, 3, 2, 2, 2])}
```

**Verification:**
```python
assert masker.n_elements_ == expected_n_regions
```

### Step 3: Assign surf_label_img = SurfaceImage(...)

```python
surf_label_img = SurfaceImage(surf_mesh, labels_data)
```

**Verification:**
```python
assert signal.shape == (n_timepoints, masker.n_elements_)
```

### Step 4: Assign mask_data = value

```python
mask_data = {'left': np.asarray([1, 1, 1, 1]), 'right': np.asarray([0, 0, 1, 1, 1])}
```

**Verification:**
```python
assert masker.labels_ == [0, 1, 2]
```

### Step 5: Assign surf_mask = SurfaceImage(...)

```python
surf_mask = SurfaceImage(surf_mesh, mask_data)
```

**Verification:**
```python
assert masker.lut_['name'].to_list() == ['Background', '1', '2']
```

### Step 6: Assign masker = SurfaceLabelsMasker(...)

```python
masker = SurfaceLabelsMasker(labels_img=surf_label_img, mask_img=surf_mask, standardize=None)
```

**Verification:**
```python
assert masker.region_names_ == {0: '1', 1: '2'}
```

### Step 7: Assign n_timepoints = 5

```python
n_timepoints = 5
```

**Verification:**
```python
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2}
```

### Step 8: Assign signal = masker.transform(...)

```python
signal = masker.transform(surf_img_2d(n_timepoints))
```

**Verification:**
```python
assert isinstance(signal, np.ndarray)
```

### Step 9: Assign expected_n_regions = 2

```python
expected_n_regions = 2
```

**Verification:**
```python
assert masker.n_elements_ == expected_n_regions
```

### Step 10: Assign masker = masker.fit(...)

```python
masker = masker.fit()
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, surf_img_2d

# Workflow
'Test transform extract signals with a mask and check warning.'
labels_data = {'left': np.asarray([1, 1, 1, 2]), 'right': np.asarray([3, 3, 2, 2, 2])}
surf_label_img = SurfaceImage(surf_mesh, labels_data)
mask_data = {'left': np.asarray([1, 1, 1, 1]), 'right': np.asarray([0, 0, 1, 1, 1])}
surf_mask = SurfaceImage(surf_mesh, mask_data)
masker = SurfaceLabelsMasker(labels_img=surf_label_img, mask_img=surf_mask, standardize=None)
with pytest.warns(UserWarning, match='the following labels were removed'):
    masker = masker.fit()
n_timepoints = 5
signal = masker.transform(surf_img_2d(n_timepoints))
assert isinstance(signal, np.ndarray)
expected_n_regions = 2
assert masker.n_elements_ == expected_n_regions
assert signal.shape == (n_timepoints, masker.n_elements_)
assert masker.labels_ == [0, 1, 2]
assert masker.lut_['name'].to_list() == ['Background', '1', '2']
assert masker.region_names_ == {0: '1', 1: '2'}
assert masker.region_ids_ == {'background': 0, 0: 1, 1: 2}
```

## Next Steps


---

*Source: test_surface_labels_masker.py:320 | Complexity: Advanced | Last updated: 2026-05-18*