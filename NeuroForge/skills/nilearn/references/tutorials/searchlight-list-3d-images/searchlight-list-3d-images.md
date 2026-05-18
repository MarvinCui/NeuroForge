# How To: Searchlight List 3D Images

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check whether searchlight works on list of 3D images.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.decoding`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check whether searchlight works on list of 3D images.'

```python
'Check whether searchlight works on list of 3D images.'
```

### Step 2: Assign frames = 30

```python
frames = 30
```

### Step 3: Assign unknown = _make_searchlight_test_data(...)

```python
data_img, _, mask_img = _make_searchlight_test_data(frames)
```

### Step 4: Assign data = rng.random(...)

```python
data = rng.random((5, 5, 5))
```

### Step 5: Assign data_img = Nifti1Image(...)

```python
data_img = Nifti1Image(data, affine=affine_eye)
```

### Step 6: Assign imgs = value

```python
imgs = [data_img] * 12
```

### Step 7: Assign y = value

```python
y = [0, 1] * 6
```

### Step 8: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img)
```

### Step 9: Call sl.fit()

```python
sl.fit(imgs, y)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Check whether searchlight works on list of 3D images.'
frames = 30
data_img, _, mask_img = _make_searchlight_test_data(frames)
data = rng.random((5, 5, 5))
data_img = Nifti1Image(data, affine=affine_eye)
imgs = [data_img] * 12
y = [0, 1] * 6
sl = searchlight.SearchLight(mask_img)
sl.fit(imgs, y)
```

## Next Steps


---

*Source: test_searchlight.py:217 | Complexity: Advanced | Last updated: 2026-05-18*