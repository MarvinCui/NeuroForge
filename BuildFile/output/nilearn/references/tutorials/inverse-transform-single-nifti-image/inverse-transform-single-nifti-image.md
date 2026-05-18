# How To: Inverse Transform Single Nifti Image

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test inverse transform single nifti image

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
# Fixtures: method, n_parcel, image_2
```

## Step-by-Step Guide

### Step 1: Assign parcellate = Parcellations(...)

```python
parcellate = Parcellations(method=method, n_parcels=n_parcel)
```

**Verification:**
```python
assert parcellate.labels_img_ is not None
```

### Step 2: Call parcellate.fit()

```python
parcellate.fit(image_2)
```

**Verification:**
```python
assert isinstance(fmri_reduced, np.ndarray)
```

### Step 3: Assign fmri_reduced = parcellate.transform(...)

```python
fmri_reduced = parcellate.transform(image_2)
```

**Verification:**
```python
assert fmri_reduced.shape == (10, n_parcel)
```

### Step 4: Assign fmri_compressed = parcellate.inverse_transform(...)

```python
fmri_compressed = parcellate.inverse_transform(fmri_reduced)
```

**Verification:**
```python
assert isinstance(fmri_compressed, Nifti1Image)
```

### Step 5: Assign fmri_compressed = parcellate.inverse_transform(...)

```python
fmri_compressed = parcellate.inverse_transform([fmri_reduced])
```

**Verification:**
```python
assert fmri_compressed.shape == image_2.shape
```


## Complete Example

```python
# Setup
# Fixtures: method, n_parcel, image_2

# Workflow
parcellate = Parcellations(method=method, n_parcels=n_parcel)
parcellate.fit(image_2)
assert parcellate.labels_img_ is not None
fmri_reduced = parcellate.transform(image_2)
assert isinstance(fmri_reduced, np.ndarray)
assert fmri_reduced.shape == (10, n_parcel)
fmri_compressed = parcellate.inverse_transform(fmri_reduced)
assert isinstance(fmri_compressed, Nifti1Image)
assert fmri_compressed.shape == image_2.shape
fmri_compressed = parcellate.inverse_transform([fmri_reduced])
assert isinstance(fmri_compressed, Nifti1Image)
assert fmri_compressed.shape == image_2.shape
```

## Next Steps


---

*Source: test_parcellations.py:367 | Complexity: Intermediate | Last updated: 2026-05-18*