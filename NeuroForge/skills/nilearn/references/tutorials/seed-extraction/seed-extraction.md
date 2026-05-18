# How To: Seed Extraction

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test seed extraction.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test seed extraction.'

```python
'Test seed extraction.'
```

**Verification:**
```python
assert_array_equal(s[:, 0], data[1, 1, 1])
```

### Step 2: Assign data = rng.random(...)

```python
data = rng.random((3, 3, 3, 5))
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([(1, 1, 1)], standardize=None)
```

### Step 5: Call masker.fit()

```python
masker.fit()
```

### Step 6: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(s[:, 0], data[1, 1, 1])
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Test seed extraction.'
data = rng.random((3, 3, 3, 5))
img = Nifti1Image(data, affine_eye)
masker = NiftiSpheresMasker([(1, 1, 1)], standardize=None)
masker.fit()
s = masker.transform(img)
assert_array_equal(s[:, 0], data[1, 1, 1])
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:61 | Complexity: Intermediate | Last updated: 2026-05-18*