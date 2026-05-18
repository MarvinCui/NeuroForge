# How To: Fit Transform With Confounds

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fit transform with confounds

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.maskers`
- `nilearn.regions.parcellations`
- `nilearn.surface`
- `nilearn.surface.tests.test_surface`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: method, n_parcel, image_2, rng
```

## Step-by-Step Guide

### Step 1: Assign fmri_imgs = value

```python
fmri_imgs = [image_2] * 3
```

**Verification:**
```python
assert isinstance(signals, list)
```

### Step 2: Assign confounds = rng.standard_normal(...)

```python
confounds = rng.standard_normal(size=(10, 3))
```

**Verification:**
```python
assert signals[0].shape == (10, n_parcel)
```

### Step 3: Assign confounds_list = value

```python
confounds_list = [confounds] * 3
```

### Step 4: Assign parcellator = Parcellations(...)

```python
parcellator = Parcellations(method=method, n_parcels=n_parcel)
```

### Step 5: Assign signals = parcellator.fit_transform(...)

```python
signals = parcellator.fit_transform(fmri_imgs, confounds=confounds_list)
```

**Verification:**
```python
assert isinstance(signals, list)
```


## Complete Example

```python
# Setup
# Fixtures: method, n_parcel, image_2, rng

# Workflow
fmri_imgs = [image_2] * 3
confounds = rng.standard_normal(size=(10, 3))
confounds_list = [confounds] * 3
parcellator = Parcellations(method=method, n_parcels=n_parcel)
signals = parcellator.fit_transform(fmri_imgs, confounds=confounds_list)
assert isinstance(signals, list)
assert signals[0].shape == (10, n_parcel)
```

## Next Steps


---

*Source: test_parcellations.py:351 | Complexity: Intermediate | Last updated: 2026-05-18*