# How To: Transform Single 3D Input Images

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test fit_transform single 3D image.

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

### Step 1: 'Test fit_transform single 3D image.'

```python
'Test fit_transform single 3D image.'
```

**Verification:**
```python
assert isinstance(X, np.ndarray)
```

### Step 2: Assign data = np.ones(...)

```python
data = np.ones((10, 11, 12))
```

**Verification:**
```python
assert X.shape == (1, 20)
```

### Step 3: Assign unknown = 2

```python
data[6, 7, 8] = 2
```

### Step 4: Assign unknown = 3

```python
data[9, 10, 11] = 3
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine=affine_eye)
```

### Step 6: Assign parcellate = Parcellations(...)

```python
parcellate = Parcellations(method='ward', n_parcels=20)
```

### Step 7: Assign X = parcellate.fit_transform(...)

```python
X = parcellate.fit_transform(img)
```

**Verification:**
```python
assert isinstance(X, np.ndarray)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test fit_transform single 3D image.'
data = np.ones((10, 11, 12))
data[6, 7, 8] = 2
data[9, 10, 11] = 3
img = Nifti1Image(data, affine=affine_eye)
parcellate = Parcellations(method='ward', n_parcels=20)
X = parcellate.fit_transform(img)
assert isinstance(X, np.ndarray)
assert X.shape == (1, 20)
```

## Next Steps


---

*Source: test_parcellations.py:396 | Complexity: Intermediate | Last updated: 2026-05-18*