# How To: Check Parameters Transform

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check parameters transform

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
# Fixtures: image_2, rng
```

## Step-by-Step Guide

### Step 1: Assign confounds = rng.standard_normal(...)

```python
confounds = rng.standard_normal(size=(10, 3))
```

**Verification:**
```python
assert isinstance(imgs, (list, tuple))
```

### Step 2: Assign unknown = _check_parameters_transform(...)

```python
imgs, confounds, single_subject = _check_parameters_transform(image_2, confounds)
```

**Verification:**
```python
assert isinstance(confounds, (list, tuple))
```

### Step 3: Assign unknown = _check_parameters_transform(...)

```python
imgs, confounds, single_subject = _check_parameters_transform(image_2, pd.DataFrame(np.array(confounds)[0]))
```

**Verification:**
```python
assert single_subject
```

### Step 4: Assign fmri_imgs = value

```python
fmri_imgs = [image_2] * 3
```

**Verification:**
```python
assert isinstance(confounds, (list, tuple))
```

### Step 5: Assign confounds_list = value

```python
confounds_list = [confounds] * 3
```

**Verification:**
```python
assert imgs == fmri_imgs
```

### Step 6: Assign unknown = _check_parameters_transform(...)

```python
imgs, confounds, _ = _check_parameters_transform(fmri_imgs, confounds_list)
```

**Verification:**
```python
assert confounds_list == confounds
```

### Step 7: Assign msg = 'Number of confounds given does not match with the given number of images'

```python
msg = 'Number of confounds given does not match with the given number of images'
```

### Step 8: Assign not_match_confounds_list = value

```python
not_match_confounds_list = [confounds] * 2
```

### Step 9: Call _check_parameters_transform()

```python
_check_parameters_transform(fmri_imgs, not_match_confounds_list)
```


## Complete Example

```python
# Setup
# Fixtures: image_2, rng

# Workflow
confounds = rng.standard_normal(size=(10, 3))
imgs, confounds, single_subject = _check_parameters_transform(image_2, confounds)
assert isinstance(imgs, (list, tuple))
assert isinstance(confounds, (list, tuple))
assert single_subject
imgs, confounds, single_subject = _check_parameters_transform(image_2, pd.DataFrame(np.array(confounds)[0]))
assert isinstance(confounds, (list, tuple))
fmri_imgs = [image_2] * 3
confounds_list = [confounds] * 3
imgs, confounds, _ = _check_parameters_transform(fmri_imgs, confounds_list)
assert imgs == fmri_imgs
assert confounds_list == confounds
msg = 'Number of confounds given does not match with the given number of images'
not_match_confounds_list = [confounds] * 2
with pytest.raises(ValueError, match=msg):
    _check_parameters_transform(fmri_imgs, not_match_confounds_list)
```

## Next Steps


---

*Source: test_parcellations.py:272 | Complexity: Advanced | Last updated: 2026-05-18*