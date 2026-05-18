# How To: Searchlight Mask Far From Signal

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test searchlight mask far from signal

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
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: Assign frames = 30

```python
frames = 30
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 0
```

### Step 2: Assign unknown = _make_searchlight_test_data(...)

```python
data_img, cond, mask_img = _make_searchlight_test_data(frames)
```

### Step 3: Assign unknown = define_cross_validation(...)

```python
cv, n_jobs = define_cross_validation()
```

### Step 4: Assign process_mask = np.zeros(...)

```python
process_mask = np.zeros((5, 5, 5), dtype=bool)
```

### Step 5: Assign unknown = True

```python
process_mask[0, 0, 0] = True
```

### Step 6: Assign process_mask_img = Nifti1Image(...)

```python
process_mask_img = Nifti1Image(process_mask.astype('uint8'), affine_eye)
```

### Step 7: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img, process_mask_img=process_mask_img, radius=0.5, n_jobs=n_jobs, scoring='accuracy', cv=cv)
```

### Step 8: Call sl.fit()

```python
sl.fit(data_img, y=cond)
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 0
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
frames = 30
data_img, cond, mask_img = _make_searchlight_test_data(frames)
cv, n_jobs = define_cross_validation()
process_mask = np.zeros((5, 5, 5), dtype=bool)
process_mask[0, 0, 0] = True
process_mask_img = Nifti1Image(process_mask.astype('uint8'), affine_eye)
sl = searchlight.SearchLight(mask_img, process_mask_img=process_mask_img, radius=0.5, n_jobs=n_jobs, scoring='accuracy', cv=cv)
sl.fit(data_img, y=cond)
assert np.where(sl.scores_ == 1)[0].size == 0
```

## Next Steps


---

*Source: test_searchlight.py:126 | Complexity: Advanced | Last updated: 2026-05-18*