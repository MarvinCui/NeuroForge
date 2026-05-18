# How To: Process Mask Shape Mismatch

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test SearchLight with mismatched process mask and image dimensions.

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

### Step 1: 'Test SearchLight with mismatched process mask and image dimensions.'

```python
'Test SearchLight with mismatched process mask and image dimensions.'
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
assert sl.scores_.shape == process_mask_img.shape
```

### Step 3: Assign unknown = _make_searchlight_test_data(...)

```python
data_img, cond, mask_img = _make_searchlight_test_data(frames)
```

### Step 4: Assign process_mask_img = Nifti1Image(...)

```python
process_mask_img = Nifti1Image(np.ones((4, 4, 4), dtype='uint8'), np.eye(4))
```

### Step 5: Assign sl = searchlight.SearchLight(...)

```python
sl = searchlight.SearchLight(mask_img=mask_img, process_mask_img=process_mask_img, radius=1.0)
```

### Step 6: Call sl.fit()

```python
sl.fit(data_img, y=cond)
```

**Verification:**
```python
assert sl.scores_ is not None
```


## Complete Example

```python
# Workflow
'Test SearchLight with mismatched process mask and image dimensions.'
frames = 20
data_img, cond, mask_img = _make_searchlight_test_data(frames)
process_mask_img = Nifti1Image(np.ones((4, 4, 4), dtype='uint8'), np.eye(4))
sl = searchlight.SearchLight(mask_img=mask_img, process_mask_img=process_mask_img, radius=1.0)
sl.fit(data_img, y=cond)
assert sl.scores_ is not None
assert sl.scores_.shape == process_mask_img.shape
```

## Next Steps


---

*Source: test_searchlight.py:279 | Complexity: Intermediate | Last updated: 2026-05-18*