# How To: Parcellation With Surface And Confounds

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if parcellation works on surface with confounds.

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
# Fixtures: method, rng, surface_img_for_parcellation, n_samples
```

## Step-by-Step Guide

### Step 1: 'Test if parcellation works on surface with confounds.'

```python
'Test if parcellation works on surface with confounds.'
```

**Verification:**
```python
assert parcellate.n_elements_ == n_parcels
```

### Step 2: Assign confounds = rng.standard_normal(...)

```python
confounds = rng.standard_normal(size=(n_samples, 3))
```

**Verification:**
```python
assert X_transformed.shape == (n_samples, n_parcels)
```

### Step 3: Assign n_parcels = 5

```python
n_parcels = 5
```

### Step 4: Assign parcellate = Parcellations(...)

```python
parcellate = Parcellations(method=method, n_parcels=n_parcels)
```

### Step 5: Assign X_transformed = parcellate.fit_transform(...)

```python
X_transformed = parcellate.fit_transform(surface_img_for_parcellation, confounds=[confounds])
```

**Verification:**
```python
assert parcellate.n_elements_ == n_parcels
```


## Complete Example

```python
# Setup
# Fixtures: method, rng, surface_img_for_parcellation, n_samples

# Workflow
'Test if parcellation works on surface with confounds.'
confounds = rng.standard_normal(size=(n_samples, 3))
n_parcels = 5
parcellate = Parcellations(method=method, n_parcels=n_parcels)
X_transformed = parcellate.fit_transform(surface_img_for_parcellation, confounds=[confounds])
assert parcellate.n_elements_ == n_parcels
assert X_transformed.shape == (n_samples, n_parcels)
```

## Next Steps


---

*Source: test_parcellations.py:477 | Complexity: Intermediate | Last updated: 2026-05-18*