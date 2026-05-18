# How To: Searchlight Small Radius

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test searchlight small radius

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign frames = 30

```python
frames = 30
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 1
```

### Step 2: Assign unknown = _make_searchlight_test_data(...)

```python
data_img, cond, mask_img = _make_searchlight_test_data(frames)
```

**Verification:**
```python
assert sl.scores_[2, 2, 2] == 1.0
```

### Step 3: Assign unknown = define_cross_validation(...)

```python
cv, n_jobs = define_cross_validation()
```

### Step 4: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img, process_mask_img=mask_img, radius=0.5, n_jobs=n_jobs, scoring='accuracy', cv=cv, verbose=0)
```

### Step 5: Call sl.fit()

```python
sl.fit(data_img, y=cond)
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 1
```


## Complete Example

```python
# Workflow
frames = 30
data_img, cond, mask_img = _make_searchlight_test_data(frames)
cv, n_jobs = define_cross_validation()
sl = searchlight.SearchLight(mask_img, process_mask_img=mask_img, radius=0.5, n_jobs=n_jobs, scoring='accuracy', cv=cv, verbose=0)
sl.fit(data_img, y=cond)
assert np.where(sl.scores_ == 1)[0].size == 1
assert sl.scores_[2, 2, 2] == 1.0
```

## Next Steps


---

*Source: test_searchlight.py:105 | Complexity: Intermediate | Last updated: 2026-05-18*