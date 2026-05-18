# How To: Remove Small Regions

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove small regions

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `scipy.ndimage`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.regions`
- `nilearn.regions.region_extractor`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: Assign data = np.array(...)

```python
data = np.array([[[0.0, 1.0, 0.0], [0.0, 1.0, 1.0], [0.0, 0.0, 0.0]], [[0.0, 0.0, 0.0], [1.0, 0.0, 0.0], [0.0, 1.0, 0.0]], [[0.0, 0.0, 1.0], [1.0, 0.0, 0.0], [0.0, 1.0, 1.0]]])
```

**Verification:**
```python
assert sum_removed_data < sum_label_data
```

### Step 2: Assign unknown = label(...)

```python
label_map, _ = label(data)
```

### Step 3: Assign sum_label_data = np.sum(...)

```python
sum_label_data = np.sum(label_map)
```

### Step 4: Assign min_size = 10

```python
min_size = 10
```

### Step 5: Assign removed_data = _remove_small_regions(...)

```python
removed_data = _remove_small_regions(label_map, affine_eye, min_size)
```

### Step 6: Assign sum_removed_data = np.sum(...)

```python
sum_removed_data = np.sum(removed_data)
```

**Verification:**
```python
assert sum_removed_data < sum_label_data
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
data = np.array([[[0.0, 1.0, 0.0], [0.0, 1.0, 1.0], [0.0, 0.0, 0.0]], [[0.0, 0.0, 0.0], [1.0, 0.0, 0.0], [0.0, 1.0, 0.0]], [[0.0, 0.0, 1.0], [1.0, 0.0, 0.0], [0.0, 1.0, 1.0]]])
label_map, _ = label(data)
sum_label_data = np.sum(label_map)
min_size = 10
removed_data = _remove_small_regions(label_map, affine_eye, min_size)
sum_removed_data = np.sum(removed_data)
assert sum_removed_data < sum_label_data
```

## Next Steps


---

*Source: test_region_extractor.py:433 | Complexity: Intermediate | Last updated: 2026-05-18*