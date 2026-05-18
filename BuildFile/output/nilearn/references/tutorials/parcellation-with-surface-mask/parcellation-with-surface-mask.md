# How To: Parcellation With Surface Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if parcellation works with surface data and a mask.

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
# Fixtures: method, surface_img_for_parcellation, n_samples
```

## Step-by-Step Guide

### Step 1: 'Test if parcellation works with surface data and a mask.'

```python
'Test if parcellation works with surface data and a mask.'
```

**Verification:**
```python
assert X_transformed.shape == (n_samples, 5)
```

### Step 2: Assign mask_data = value

```python
mask_data = {'left': np.ones(surface_img_for_parcellation.mesh.parts['left'].coordinates.shape[0]).astype(bool), 'right': np.ones(surface_img_for_parcellation.mesh.parts['right'].coordinates.shape[0]).astype(bool)}
```

### Step 3: Assign mask_img = SurfaceImage(...)

```python
mask_img = SurfaceImage(mesh=surface_img_for_parcellation.mesh, data=mask_data)
```

### Step 4: Assign parcellate = Parcellations(...)

```python
parcellate = Parcellations(method=method, n_parcels=5, mask=mask_img)
```

### Step 5: Assign X_transformed = parcellate.fit_transform(...)

```python
X_transformed = parcellate.fit_transform(surface_img_for_parcellation)
```

**Verification:**
```python
assert X_transformed.shape == (n_samples, 5)
```


## Complete Example

```python
# Setup
# Fixtures: method, surface_img_for_parcellation, n_samples

# Workflow
'Test if parcellation works with surface data and a mask.'
mask_data = {'left': np.ones(surface_img_for_parcellation.mesh.parts['left'].coordinates.shape[0]).astype(bool), 'right': np.ones(surface_img_for_parcellation.mesh.parts['right'].coordinates.shape[0]).astype(bool)}
mask_img = SurfaceImage(mesh=surface_img_for_parcellation.mesh, data=mask_data)
parcellate = Parcellations(method=method, n_parcels=5, mask=mask_img)
X_transformed = parcellate.fit_transform(surface_img_for_parcellation)
assert X_transformed.shape == (n_samples, 5)
```

## Next Steps


---

*Source: test_parcellations.py:514 | Complexity: Intermediate | Last updated: 2026-05-18*