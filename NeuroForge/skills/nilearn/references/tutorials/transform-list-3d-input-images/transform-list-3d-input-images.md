# How To: Transform List 3D Input Images

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test fit_transform list 3D image.

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
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test fit_transform list 3D image.'

```python
'Test fit_transform list 3D image.'
```

**Verification:**
```python
assert isinstance(X, list)
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((10, 11, 12))
```

**Verification:**
```python
assert np.concatenate(X).shape == (2, 20)
```

### Step 3: Assign unknown = 2

```python
data[6, 7, 8] = 2
```

**Verification:**
```python
assert isinstance(imgs_, list)
```

### Step 4: Assign unknown = 3

```python
data[9, 10, 11] = 3
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine=affine_eye)
```

### Step 6: Assign imgs = value

```python
imgs = [img] * 2
```

### Step 7: Assign parcellate = Parcellations(...)

```python
parcellate = Parcellations(method='ward', n_parcels=20)
```

### Step 8: Assign X = parcellate.fit_transform(...)

```python
X = parcellate.fit_transform(imgs)
```

**Verification:**
```python
assert isinstance(X, list)
```

### Step 9: Assign imgs_ = parcellate.inverse_transform(...)

```python
imgs_ = parcellate.inverse_transform(X)
```

**Verification:**
```python
assert isinstance(imgs_, list)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test fit_transform list 3D image.'
data = np.ones((10, 11, 12))
data[6, 7, 8] = 2
data[9, 10, 11] = 3
img = Nifti1Image(data, affine=affine_eye)
imgs = [img] * 2
parcellate = Parcellations(method='ward', n_parcels=20)
X = parcellate.fit_transform(imgs)
assert isinstance(X, list)
assert np.concatenate(X).shape == (2, 20)
imgs_ = parcellate.inverse_transform(X)
assert isinstance(imgs_, list)
```

## Next Steps


---

*Source: test_parcellations.py:412 | Complexity: Advanced | Last updated: 2026-05-18*