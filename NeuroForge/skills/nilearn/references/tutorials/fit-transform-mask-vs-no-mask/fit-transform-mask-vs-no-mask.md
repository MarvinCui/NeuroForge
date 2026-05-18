# How To: Fit Transform Mask Vs No Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that fit_transform returns the different results when a mask is
used vs. when no mask is used.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_maps_img, surf_img_2d, surf_mask_1d
```

## Step-by-Step Guide

### Step 1: 'Test that fit_transform returns the different results when a mask is\n    used vs. when no mask is used.\n    '

```python
'Test that fit_transform returns the different results when a mask is\n    used vs. when no mask is used.\n    '
```

**Verification:**
```python
assert not (region_signals_with_mask == region_signals_no_mask).all()
```

### Step 2: Assign masker_with_mask = SurfaceMapsMasker.fit(...)

```python
masker_with_mask = SurfaceMapsMasker(surf_maps_img, surf_mask_1d, standardize=None).fit()
```

### Step 3: Assign region_signals_with_mask = masker_with_mask.transform(...)

```python
region_signals_with_mask = masker_with_mask.transform(surf_img_2d(50))
```

### Step 4: Assign masker_no_mask = SurfaceMapsMasker.fit(...)

```python
masker_no_mask = SurfaceMapsMasker(surf_maps_img, standardize=None).fit()
```

### Step 5: Assign region_signals_no_mask = masker_no_mask.transform(...)

```python
region_signals_no_mask = masker_no_mask.transform(surf_img_2d(50))
```

**Verification:**
```python
assert not (region_signals_with_mask == region_signals_no_mask).all()
```


## Complete Example

```python
# Setup
# Fixtures: surf_maps_img, surf_img_2d, surf_mask_1d

# Workflow
'Test that fit_transform returns the different results when a mask is\n    used vs. when no mask is used.\n    '
masker_with_mask = SurfaceMapsMasker(surf_maps_img, surf_mask_1d, standardize=None).fit()
region_signals_with_mask = masker_with_mask.transform(surf_img_2d(50))
masker_no_mask = SurfaceMapsMasker(surf_maps_img, standardize=None).fit()
region_signals_no_mask = masker_no_mask.transform(surf_img_2d(50))
assert not (region_signals_with_mask == region_signals_no_mask).all()
```

## Next Steps


---

*Source: test_surface_maps_masker.py:57 | Complexity: Intermediate | Last updated: 2026-05-18*