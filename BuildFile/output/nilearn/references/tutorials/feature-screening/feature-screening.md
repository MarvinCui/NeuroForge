# How To: Feature Screening

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that screening percentile is correctly adjusted.

For very small ROIs, all elements should be included.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `sklearn.base`
- `sklearn.feature_selection`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.decoding._utils`

**Setup Required:**
```python
# Fixtures: affine_eye, is_classif, screening_percentile, roi_size
```

## Step-by-Step Guide

### Step 1: 'Check that screening percentile is correctly adjusted.\n\n    For very small ROIs, all elements should be included.\n    '

```python
'Check that screening percentile is correctly adjusted.\n\n    For very small ROIs, all elements should be included.\n    '
```

**Verification:**
```python
assert check_feature_screening(screening_percentile, mask_img, is_classif) is None
```

### Step 2: Assign mask_img_data = np.zeros(...)

```python
mask_img_data = np.zeros((182, 218, 182))
```

**Verification:**
```python
assert select_percentile.percentile == 100
```

### Step 3: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img_data, affine=affine_eye)
```

**Verification:**
```python
assert screening_percentile <= select_percentile.percentile < 100
```

### Step 4: Assign unknown = 1

```python
mask_img_data[80:-80, 80:-80, 80:-80] = 1
```

**Verification:**
```python
assert isinstance(select_percentile, BaseEstimator)
```

### Step 5: Assign unknown = 1

```python
mask_img_data[40:-40, 40:-40, 40:-40] = 1
```

**Verification:**
```python
assert check_feature_screening(screening_percentile, mask_img, is_classif) is None
```

### Step 6: Call check_feature_screening()

```python
check_feature_screening(screening_percentile, mask_img, is_classif)
```

**Verification:**
```python
assert select_percentile.percentile == 100
```

### Step 7: Assign select_percentile = check_feature_screening(...)

```python
select_percentile = check_feature_screening(screening_percentile, mask_img, is_classif)
```

**Verification:**
```python
assert screening_percentile <= select_percentile.percentile < 100
```

### Step 8: Assign select_percentile = check_feature_screening(...)

```python
select_percentile = check_feature_screening(screening_percentile, mask_img, is_classif)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, is_classif, screening_percentile, roi_size

# Workflow
'Check that screening percentile is correctly adjusted.\n\n    For very small ROIs, all elements should be included.\n    '
mask_img_data = np.zeros((182, 218, 182))
if roi_size == 'small':
    mask_img_data[80:-80, 80:-80, 80:-80] = 1
else:
    mask_img_data[40:-40, 40:-40, 40:-40] = 1
mask_img = Nifti1Image(mask_img_data, affine=affine_eye)
if screening_percentile == 100 or screening_percentile is None:
    assert check_feature_screening(screening_percentile, mask_img, is_classif) is None
elif screening_percentile in {-1, 101}:
    with pytest.raises(ValueError):
        check_feature_screening(screening_percentile, mask_img, is_classif)
else:
    if roi_size == 'small':
        with pytest.warns(UserWarning, match="screening_percentile set to '100'"):
            select_percentile = check_feature_screening(screening_percentile, mask_img, is_classif)
        assert select_percentile.percentile == 100
    else:
        select_percentile = check_feature_screening(screening_percentile, mask_img, is_classif)
        assert screening_percentile <= select_percentile.percentile < 100
    assert isinstance(select_percentile, BaseEstimator)
```

## Next Steps


---

*Source: test_utils.py:27 | Complexity: Advanced | Last updated: 2026-05-18*