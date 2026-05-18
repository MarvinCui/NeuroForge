# How To: Get Clusters Table No Cluster Found Warning

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check warning is thrown when too high threshold or no cluster found.

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
# Fixtures: surf_img_1d, simple_stat_img
```

## Step-by-Step Guide

### Step 1: 'Check warning is thrown when too high threshold or no cluster found.'

```python
'Check warning is thrown when too high threshold or no cluster found.'
```

### Step 2: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=0)
```

### Step 3: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=0)
```

### Step 4: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=0)
```

### Step 5: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=0)
```

### Step 6: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(simple_stat_img, stat_threshold=1000)
```

### Step 7: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(surf_img_1d, stat_threshold=1000)
```

### Step 8: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(simple_stat_img, stat_threshold=4.9, cluster_threshold=1000)
```

### Step 9: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(surf_img_1d, stat_threshold=1, cluster_threshold=1000)
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d, simple_stat_img

# Workflow
'Check warning is thrown when too high threshold or no cluster found.'
with pytest.warns(UserWarning, match='But, you have given threshold=1000'):
    clusters_table = get_clusters_table(simple_stat_img, stat_threshold=1000)
validate_clusters_table(clusters_table, expected_n_cluster=0)
with pytest.warns(UserWarning, match='But, you have given threshold=1000'):
    clusters_table = get_clusters_table(surf_img_1d, stat_threshold=1000)
validate_clusters_table(clusters_table, expected_n_cluster=0)
with pytest.warns(UserWarning, match='No clusters found'):
    clusters_table = get_clusters_table(simple_stat_img, stat_threshold=4.9, cluster_threshold=1000)
validate_clusters_table(clusters_table, expected_n_cluster=0)
with pytest.warns(UserWarning, match='No clusters found'):
    clusters_table = get_clusters_table(surf_img_1d, stat_threshold=1, cluster_threshold=1000)
validate_clusters_table(clusters_table, expected_n_cluster=0)
```

## Next Steps


---

*Source: test_get_clusters_table.py:314 | Complexity: Advanced | Last updated: 2026-05-18*