# How To: Get Clusters Table Surface Real Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test cluster table generation on real surface data.

Assert that n_clusters two sided equals
sum of n_clusters one sided     with positive and negative threshold.

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
# Fixtures: stat_threshold, cluster_threshold, expected_n_cluster_two_sided
```

## Step-by-Step Guide

### Step 1: 'Test cluster table generation on real surface data.\n\n    Assert that n_clusters two sided equals\n    sum of n_clusters one sided     with positive and negative threshold.\n    '

```python
'Test cluster table generation on real surface data.\n\n    Assert that n_clusters two sided equals\n    sum of n_clusters one sided     with positive and negative threshold.\n    '
```

**Verification:**
```python
assert len(clusters_table_two_sided) == len(clusters_table_positive) + len(clusters_table_negative)
```

### Step 2: Assign stat_img = load_fsaverage_data(...)

```python
stat_img = load_fsaverage_data(mesh_type='inflated')
```

### Step 3: Assign clusters_table_two_sided = get_clusters_table(...)

```python
clusters_table_two_sided = get_clusters_table(stat_img, stat_threshold=np.abs(stat_threshold), cluster_threshold=cluster_threshold, two_sided=True)
```

### Step 4: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table_two_sided, expected_n_cluster_two_sided)
```

### Step 5: Assign clusters_table_positive = get_clusters_table(...)

```python
clusters_table_positive = get_clusters_table(stat_img, stat_threshold=np.abs(stat_threshold), cluster_threshold=cluster_threshold, two_sided=False)
```

### Step 6: Assign clusters_table_negative = get_clusters_table(...)

```python
clusters_table_negative = get_clusters_table(math_img('img*-1', img=stat_img), stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, two_sided=False)
```

**Verification:**
```python
assert len(clusters_table_two_sided) == len(clusters_table_positive) + len(clusters_table_negative)
```


## Complete Example

```python
# Setup
# Fixtures: stat_threshold, cluster_threshold, expected_n_cluster_two_sided

# Workflow
'Test cluster table generation on real surface data.\n\n    Assert that n_clusters two sided equals\n    sum of n_clusters one sided     with positive and negative threshold.\n    '
stat_img = load_fsaverage_data(mesh_type='inflated')
clusters_table_two_sided = get_clusters_table(stat_img, stat_threshold=np.abs(stat_threshold), cluster_threshold=cluster_threshold, two_sided=True)
validate_clusters_table(clusters_table_two_sided, expected_n_cluster_two_sided)
clusters_table_positive = get_clusters_table(stat_img, stat_threshold=np.abs(stat_threshold), cluster_threshold=cluster_threshold, two_sided=False)
clusters_table_negative = get_clusters_table(math_img('img*-1', img=stat_img), stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, two_sided=False)
assert len(clusters_table_two_sided) == len(clusters_table_positive) + len(clusters_table_negative)
```

## Next Steps


---

*Source: test_get_clusters_table.py:253 | Complexity: Intermediate | Last updated: 2026-05-18*