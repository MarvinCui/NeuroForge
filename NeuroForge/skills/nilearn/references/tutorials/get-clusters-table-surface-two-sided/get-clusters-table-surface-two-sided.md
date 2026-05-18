# How To: Get Clusters Table Surface Two Sided

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test n_clusters detected with two sided.

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
# Fixtures: surf_img_1d, stat_threshold, cluster_threshold, expected_n_cluster_left, expected_n_cluster_right, contain_neg_and_pos
```

## Step-by-Step Guide

### Step 1: 'Test n_clusters detected with two sided.'

```python
'Test n_clusters detected with two sided.'
```

**Verification:**
```python
assert np.any(clusters_table['Peak Stat'].to_numpy() > 0)
```

### Step 2: Assign unknown = np.asarray(...)

```python
surf_img_1d.data.parts['left'] = np.asarray([5.1, 5.2, 5.3, -5])
```

**Verification:**
```python
assert np.any(clusters_table['Peak Stat'].to_numpy() < 0)
```

### Step 3: Assign unknown = np.asarray(...)

```python
surf_img_1d.data.parts['right'] = np.asarray([0, 4, 0, 5.4, -5.2])
```

**Verification:**
```python
assert isinstance(label_maps, list)
```

### Step 4: Assign stat_img = surf_img_1d

```python
stat_img = surf_img_1d
```

**Verification:**
```python
assert all((isinstance(x, SurfaceImage) for x in label_maps))
```

### Step 5: Assign unknown = get_clusters_table(...)

```python
clusters_table, label_maps = get_clusters_table(stat_img, stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, two_sided=True, return_label_maps=True)
```

**Verification:**
```python
assert cluster_labels_positive.size == expected_n_cluster_left + 1
```

### Step 6: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster_left + expected_n_cluster_right)
```

**Verification:**
```python
assert cluster_labels_negative.size == expected_n_cluster_right + 1
```

### Step 7: Assign cluster_labels_positive = np.unique(...)

```python
cluster_labels_positive = np.unique(get_surface_data(label_maps[0]))
```

**Verification:**
```python
assert cluster_labels_positive.size == expected_n_cluster_left + 1
```

### Step 8: Assign cluster_labels_negative = np.unique(...)

```python
cluster_labels_negative = np.unique(get_surface_data(label_maps[1]))
```

**Verification:**
```python
assert cluster_labels_negative.size == expected_n_cluster_right + 1
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d, stat_threshold, cluster_threshold, expected_n_cluster_left, expected_n_cluster_right, contain_neg_and_pos

# Workflow
'Test n_clusters detected with two sided.'
surf_img_1d.data.parts['left'] = np.asarray([5.1, 5.2, 5.3, -5])
surf_img_1d.data.parts['right'] = np.asarray([0, 4, 0, 5.4, -5.2])
stat_img = surf_img_1d
clusters_table, label_maps = get_clusters_table(stat_img, stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, two_sided=True, return_label_maps=True)
validate_clusters_table(clusters_table, expected_n_cluster_left + expected_n_cluster_right)
if contain_neg_and_pos:
    assert np.any(clusters_table['Peak Stat'].to_numpy() > 0)
    assert np.any(clusters_table['Peak Stat'].to_numpy() < 0)
assert isinstance(label_maps, list)
assert all((isinstance(x, SurfaceImage) for x in label_maps))
cluster_labels_positive = np.unique(get_surface_data(label_maps[0]))
assert cluster_labels_positive.size == expected_n_cluster_left + 1
cluster_labels_negative = np.unique(get_surface_data(label_maps[1]))
assert cluster_labels_negative.size == expected_n_cluster_right + 1
```

## Next Steps


---

*Source: test_get_clusters_table.py:205 | Complexity: Advanced | Last updated: 2026-05-18*