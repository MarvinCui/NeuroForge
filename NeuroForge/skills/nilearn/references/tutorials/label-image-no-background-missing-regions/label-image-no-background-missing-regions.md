# How To: Label Image No Background Missing Regions

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test label image with no background.

Compare behavior when background is present in label image
(background_label=1) or not (background_label=0).

Regression test for https://github.com/nilearn/nilearn/issues/5596

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
# Fixtures: surf_mesh, surf_img_2d, background_label, n_expected_regions, kwargs
```

## Step-by-Step Guide

### Step 1: 'Test label image with no background.\n\n    Compare behavior when background is present in label image\n    (background_label=1) or not (background_label=0).\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5596\n    '

```python
'Test label image with no background.\n\n    Compare behavior when background is present in label image\n    (background_label=1) or not (background_label=0).\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5596\n    '
```

**Verification:**
```python
assert list(kwargs['lut'].columns) == list(labels_masker.lut_.columns)
```

### Step 2: Assign data = value

```python
data = {'left': np.asarray([3, 3, 1, 1]), 'right': np.asarray([1, 1, 3, 2, 3])}
```

**Verification:**
```python
assert masked_data.shape[1] == n_expected_regions
```

### Step 3: Assign label_img = SurfaceImage(...)

```python
label_img = SurfaceImage(surf_mesh, data)
```

**Verification:**
```python
assert len(labels_masker.region_names_) == n_expected_regions
```

### Step 4: Assign labels_masker = SurfaceLabelsMasker.fit(...)

```python
labels_masker = SurfaceLabelsMasker(labels_img=label_img, background_label=background_label, standardize=None, **kwargs).fit()
```

**Verification:**
```python
assert 'Background' in labels_masker.lut_['name'].to_list()
```

### Step 5: Assign masked_data = labels_masker.transform(...)

```python
masked_data = labels_masker.transform(surf_img_2d(2))
```

**Verification:**
```python
assert len(labels_masker.labels_) == n_expected_regions + 1
```


## Complete Example

```python
# Setup
# Fixtures: surf_mesh, surf_img_2d, background_label, n_expected_regions, kwargs

# Workflow
'Test label image with no background.\n\n    Compare behavior when background is present in label image\n    (background_label=1) or not (background_label=0).\n\n    Regression test for https://github.com/nilearn/nilearn/issues/5596\n    '
data = {'left': np.asarray([3, 3, 1, 1]), 'right': np.asarray([1, 1, 3, 2, 3])}
label_img = SurfaceImage(surf_mesh, data)
labels_masker = SurfaceLabelsMasker(labels_img=label_img, background_label=background_label, standardize=None, **kwargs).fit()
if 'lut' in kwargs:
    assert list(kwargs['lut'].columns) == list(labels_masker.lut_.columns)
masked_data = labels_masker.transform(surf_img_2d(2))
assert masked_data.shape[1] == n_expected_regions
assert len(labels_masker.region_names_) == n_expected_regions
if background_label == 1:
    assert 'Background' in labels_masker.lut_['name'].to_list()
    assert len(labels_masker.labels_) == n_expected_regions + 1
    assert len(labels_masker.region_ids_) == n_expected_regions + 1
else:
    assert 'Background' not in labels_masker.lut_['name'].to_list()
    assert len(labels_masker.labels_) == n_expected_regions
    assert len(labels_masker.region_ids_) == n_expected_regions
```

## Next Steps


---

*Source: test_surface_labels_masker.py:223 | Complexity: Intermediate | Last updated: 2026-05-18*