# How To: Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Throw error when allow_overlap=False and some spheres overlap.

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

### Step 1: 'Throw error when allow_overlap=False and some spheres overlap.'

```python
'Throw error when allow_overlap=False and some spheres overlap.'
```

### Step 2: Assign shape = value

```python
shape = (5, 5, 5)
```

### Step 3: Assign data = rng.random(...)

```python
data = rng.random((*shape, 5))
```

### Step 4: Assign fmri_img = Nifti1Image(...)

```python
fmri_img = Nifti1Image(data, affine_eye)
```

### Step 5: Assign seeds = value

```python
seeds = [(0, 0, 0), (2, 2, 2)]
```

### Step 6: Assign overlapping_masker = NiftiSpheresMasker(...)

```python
overlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=True, standardize=None)
```

### Step 7: Call overlapping_masker.fit_transform()

```python
overlapping_masker.fit_transform(fmri_img)
```

### Step 8: Assign overlapping_masker = NiftiSpheresMasker(...)

```python
overlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=True, standardize=None)
```

### Step 9: Call overlapping_masker.fit_transform()

```python
overlapping_masker.fit_transform(fmri_img)
```

### Step 10: Assign noverlapping_masker = NiftiSpheresMasker(...)

```python
noverlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=False, standardize=None)
```

### Step 11: Call noverlapping_masker.fit_transform()

```python
noverlapping_masker.fit_transform(fmri_img)
```

### Step 12: Assign noverlapping_masker = NiftiSpheresMasker(...)

```python
noverlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=False, standardize=None)
```

### Step 13: Call noverlapping_masker.fit_transform()

```python
noverlapping_masker.fit_transform(fmri_img)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Throw error when allow_overlap=False and some spheres overlap.'
shape = (5, 5, 5)
data = rng.random((*shape, 5))
fmri_img = Nifti1Image(data, affine_eye)
seeds = [(0, 0, 0), (2, 2, 2)]
overlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=True, standardize=None)
overlapping_masker.fit_transform(fmri_img)
overlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=True, standardize=None)
overlapping_masker.fit_transform(fmri_img)
noverlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=False, standardize=None)
noverlapping_masker.fit_transform(fmri_img)
noverlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=False, standardize=None)
with pytest.raises(ValueError, match='Overlap detected'):
    noverlapping_masker.fit_transform(fmri_img)
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:166 | Complexity: Advanced | Last updated: 2026-05-18*