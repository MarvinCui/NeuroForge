# How To: Get Clusters Table Surface

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test n_clusters detected.

Also check negative thresholds for one sided.

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
# Fixtures: surf_img_1d, stat_threshold, cluster_threshold, expected_n_cluster
```

## Step-by-Step Guide

### Step 1: 'Test n_clusters detected.\n\n    Also check negative thresholds for one sided.\n    '

```python
'Test n_clusters detected.\n\n    Also check negative thresholds for one sided.\n    '
```

**Verification:**
```python
assert isinstance(label_maps, list)
```

### Step 2: Assign unknown = np.asarray(...)

```python
surf_img_1d.data.parts['left'] = np.asarray([5.1, 5.2, 5.3, -5])
```

**Verification:**
```python
assert all((isinstance(x, SurfaceImage) for x in label_maps))
```

### Step 3: Assign unknown = np.asarray(...)

```python
surf_img_1d.data.parts['right'] = np.asarray([0, 4, 0, 5.4, -5.2])
```

**Verification:**
```python
assert len(label_maps) == 1
```

### Step 4: Assign stat_img = surf_img_1d

```python
stat_img = surf_img_1d
```

**Verification:**
```python
assert cluster_labels.size == expected_n_cluster + 1
```

### Step 5: Assign unknown = get_clusters_table(...)

```python
clusters_table, label_maps = get_clusters_table(stat_img, stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, return_label_maps=True)
```

### Step 6: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster)
```

**Verification:**
```python
assert isinstance(label_maps, list)
```

### Step 7: Assign cluster_labels = np.unique(...)

```python
cluster_labels = np.unique(get_surface_data(label_maps[0]))
```

**Verification:**
```python
assert cluster_labels.size == expected_n_cluster + 1
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_1d, stat_threshold, cluster_threshold, expected_n_cluster

# Workflow
'Test n_clusters detected.\n\n    Also check negative thresholds for one sided.\n    '
surf_img_1d.data.parts['left'] = np.asarray([5.1, 5.2, 5.3, -5])
surf_img_1d.data.parts['right'] = np.asarray([0, 4, 0, 5.4, -5.2])
stat_img = surf_img_1d
clusters_table, label_maps = get_clusters_table(stat_img, stat_threshold=stat_threshold, cluster_threshold=cluster_threshold, return_label_maps=True)
validate_clusters_table(clusters_table, expected_n_cluster)
assert isinstance(label_maps, list)
assert all((isinstance(x, SurfaceImage) for x in label_maps))
assert len(label_maps) == 1
cluster_labels = np.unique(get_surface_data(label_maps[0]))
assert cluster_labels.size == expected_n_cluster + 1
```

## Next Steps


---

*Source: test_get_clusters_table.py:164 | Complexity: Intermediate | Last updated: 2026-05-18*