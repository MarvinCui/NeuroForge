# How To: Inverse Transform With Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test inverse_transform with mask: inverted image's shape, warning if
mask removes labels and data corresponding to removed labels is zeros.

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

### Step 1: "Test inverse_transform with mask: inverted image's shape, warning if\n    mask removes labels and data corresponding to removed labels is zeros.\n    "

```python
"Test inverse_transform with mask: inverted image's shape, warning if\n    mask removes labels and data corresponding to removed labels is zeros.\n    "
```

**Verification:**
```python
assert img_inverted.shape == surf_img_2d(n_timepoints).shape
```

### Step 2: Assign labels_data = value

```python
labels_data = {'left': np.asarray([1, 1, 1, 2]), 'right': np.asarray([3, 3, 2, 2, 2])}
```

**Verification:**
```python
assert np.all(img_inverted.data.parts['left'][-1, :] == 0)
```

### Step 3: Assign surf_label_img = SurfaceImage(...)

```python
surf_label_img = SurfaceImage(surf_mesh, labels_data)
```

**Verification:**
```python
assert np.all(img_inverted.data.parts['right'][2:, :] == 0)
```

### Step 4: Assign mask_data = value

```python
mask_data = {'left': np.asarray([1, 1, 1, 0]), 'right': np.asarray([1, 1, 0, 0, 0])}
```

### Step 5: Assign surf_mask = SurfaceImage(...)

```python
surf_mask = SurfaceImage(surf_mesh, mask_data)
```

### Step 6: Assign masker = SurfaceLabelsMasker(...)

```python
masker = SurfaceLabelsMasker(labels_img=surf_label_img, mask_img=surf_mask, standardize=None)
```

### Step 7: Assign n_timepoints = 5

```python
n_timepoints = 5
```

### Step 8: Assign signal = masker.transform(...)

```python
signal = masker.transform(surf_img_2d(n_timepoints))
```

### Step 9: Assign img_inverted = masker.inverse_transform(...)

```python
img_inverted = masker.inverse_transform(signal)
```

**Verification:**
```python
assert img_inverted.shape == surf_img_2d(n_timepoints).shape
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
"Test inverse_transform with mask: inverted image's shape, warning if\n    mask removes labels and data corresponding to removed labels is zeros.\n    "
labels_data = {'left': np.asarray([1, 1, 1, 2]), 'right': np.asarray([3, 3, 2, 2, 2])}
surf_label_img = SurfaceImage(surf_mesh, labels_data)
mask_data = {'left': np.asarray([1, 1, 1, 0]), 'right': np.asarray([1, 1, 0, 0, 0])}
surf_mask = SurfaceImage(surf_mesh, mask_data)
masker = SurfaceLabelsMasker(labels_img=surf_label_img, mask_img=surf_mask, standardize=None)
with pytest.warns(UserWarning, match='the following labels were removed'):
    masker = masker.fit()
n_timepoints = 5
signal = masker.transform(surf_img_2d(n_timepoints))
img_inverted = masker.inverse_transform(signal)
assert img_inverted.shape == surf_img_2d(n_timepoints).shape
assert np.all(img_inverted.data.parts['left'][-1, :] == 0)
assert np.all(img_inverted.data.parts['right'][2:, :] == 0)
```

## Next Steps


---

*Source: test_surface_labels_masker.py:667 | Complexity: Advanced | Last updated: 2026-05-18*