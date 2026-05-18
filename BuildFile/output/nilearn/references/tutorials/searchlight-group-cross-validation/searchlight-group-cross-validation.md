# How To: Searchlight Group Cross Validation

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check several valid cv scheme.

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
# Fixtures: rng, frames, cv
```

## Step-by-Step Guide

### Step 1: 'Check several valid cv scheme.'

```python
'Check several valid cv scheme.'
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 7
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
_, n_jobs = define_cross_validation()
```

### Step 4: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img, process_mask_img=mask_img, radius=1, n_jobs=n_jobs, scoring='accuracy', cv=cv)
```

### Step 5: Assign groups = rng.permutation(...)

```python
groups = rng.permutation(np.arange(frames, dtype=int) > frames // 2)
```

### Step 6: Call sl.fit()

```python
sl.fit(data_img, y=cond, groups=groups)
```

**Verification:**
```python
assert np.where(sl.scores_ == 1)[0].size == 7
```

### Step 7: Assign groups = None

```python
groups = None
```


## Complete Example

```python
# Setup
# Fixtures: rng, frames, cv

# Workflow
'Check several valid cv scheme.'
data_img, cond, mask_img = _make_searchlight_test_data(frames)
_, n_jobs = define_cross_validation()
sl = searchlight.SearchLight(mask_img, process_mask_img=mask_img, radius=1, n_jobs=n_jobs, scoring='accuracy', cv=cv)
groups = rng.permutation(np.arange(frames, dtype=int) > frames // 2)
if cv in [5, None]:
    groups = None
sl.fit(data_img, y=cond, groups=groups)
assert np.where(sl.scores_ == 1)[0].size == 7
assert sl.scores_[2, 2, 2] == 1.0
```

## Next Steps


---

*Source: test_searchlight.py:195 | Complexity: Intermediate | Last updated: 2026-05-18*