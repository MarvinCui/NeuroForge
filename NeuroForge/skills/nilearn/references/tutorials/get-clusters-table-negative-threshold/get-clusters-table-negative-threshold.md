# How To: Get Clusters Table Negative Threshold

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that one sided negative thresholds are handled well.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `copy`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn.datasets`
- `nilearn.image`
- `nilearn.reporting.get_clusters_table`
- `nilearn.surface.surface`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: shape, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check that one sided negative thresholds are handled well.'

```python
'Check that one sided negative thresholds are handled well.'
```

**Verification:**
```python
assert_array_equal(stat_img.get_fdata(), data_orig)
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros(shape)
```

### Step 3: Assign unknown = 5.0

```python
data[2:4, 5:7, 6:8] = 5.0
```

### Step 4: Assign unknown = value

```python
data[4:6, 7:9, 8:10] = -5.0
```

### Step 5: Assign stat_img = Nifti1Image(...)

```python
stat_img = Nifti1Image(data, affine_eye)
```

### Step 6: Assign data_orig = deepcopy(...)

```python
data_orig = deepcopy(data)
```

### Step 7: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(stat_img, stat_threshold=-1, cluster_threshold=0, two_sided=False)
```

### Step 8: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=1)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(stat_img.get_fdata(), data_orig)
```


## Complete Example

```python
# Setup
# Fixtures: shape, affine_eye

# Workflow
'Check that one sided negative thresholds are handled well.'
data = np.zeros(shape)
data[2:4, 5:7, 6:8] = 5.0
data[4:6, 7:9, 8:10] = -5.0
stat_img = Nifti1Image(data, affine_eye)
data_orig = deepcopy(data)
clusters_table = get_clusters_table(stat_img, stat_threshold=-1, cluster_threshold=0, two_sided=False)
validate_clusters_table(clusters_table, expected_n_cluster=1)
assert_array_equal(stat_img.get_fdata(), data_orig)
```

## Next Steps


---

*Source: test_get_clusters_table.py:341 | Complexity: Advanced | Last updated: 2026-05-18*