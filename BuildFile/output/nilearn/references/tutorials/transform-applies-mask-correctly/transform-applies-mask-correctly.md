# How To: Transform Applies Mask Correctly

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if `transform()` applies the mask correctly.

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

### Step 1: 'Test if `transform()` applies the mask correctly.'

```python
'Test if `transform()` applies the mask correctly.'
```

**Verification:**
```python
assert sl.scores_ is not None
```

### Step 2: Assign frames = 20

```python
frames = 20
```

**Verification:**
```python
assert sl.process_mask_ is not None
```

### Step 3: Assign unknown = _make_searchlight_test_data(...)

```python
data_img, cond, mask_img = _make_searchlight_test_data(frames)
```

**Verification:**
```python
assert transformed_scores is not None
```

### Step 4: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img, radius=1.0)
```

**Verification:**
```python
assert transformed_scores.shape == (5, 5, 5)
```

### Step 5: Call sl.fit()

```python
sl.fit(data_img, y=cond)
```

**Verification:**
```python
assert transformed_scores.size > 0
```

### Step 6: Assign transformed_scores = sl.transform(...)

```python
transformed_scores = sl.transform(data_img)
```

**Verification:**
```python
assert transformed_scores is not None
```


## Complete Example

```python
# Workflow
'Test if `transform()` applies the mask correctly.'
frames = 20
data_img, cond, mask_img = _make_searchlight_test_data(frames)
sl = searchlight.SearchLight(mask_img, radius=1.0)
sl.fit(data_img, y=cond)
assert sl.scores_ is not None
assert sl.process_mask_ is not None
transformed_scores = sl.transform(data_img)
assert transformed_scores is not None
assert transformed_scores.shape == (5, 5, 5)
assert transformed_scores.size > 0
```

## Next Steps


---

*Source: test_searchlight.py:259 | Complexity: Intermediate | Last updated: 2026-05-18*