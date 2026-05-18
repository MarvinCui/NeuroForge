# How To: Cluster Nearest Neighbor

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that _cluster_nearest_neighbor preserves within-cluster voxels,        projects voxels to the correct cluster,        and handles singleton clusters.
    

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
# Fixtures: shape
```

## Step-by-Step Guide

### Step 1: 'Check that _cluster_nearest_neighbor preserves within-cluster voxels,        projects voxels to the correct cluster,        and handles singleton clusters.\n    '

```python
'Check that _cluster_nearest_neighbor preserves within-cluster voxels,        projects voxels to the correct cluster,        and handles singleton clusters.\n    '
```

**Verification:**
```python
assert np.array_equal(nbrs, np.array([[4, 7, 5], [4, 5, 5], [4, 2, 6]]))
```

### Step 2: Assign labeled = np.zeros(...)

```python
labeled = np.zeros(shape)
```

### Step 3: Assign unknown = 1

```python
labeled[:, 5:, :] = 1
```

### Step 4: Assign unknown = 2

```python
labeled[4, 2, 6] = 2
```

### Step 5: Assign labels_index = np.array(...)

```python
labels_index = np.array([1, 1, 2])
```

### Step 6: Assign ijk = np.array(...)

```python
ijk = np.array([[4, 7, 5], [4, 2, 5], [4, 3, 6]])
```

### Step 7: Assign nbrs = _cluster_nearest_neighbor(...)

```python
nbrs = _cluster_nearest_neighbor(ijk, labels_index, labeled)
```

**Verification:**
```python
assert np.array_equal(nbrs, np.array([[4, 7, 5], [4, 5, 5], [4, 2, 6]]))
```


## Complete Example

```python
# Setup
# Fixtures: shape

# Workflow
'Check that _cluster_nearest_neighbor preserves within-cluster voxels,        projects voxels to the correct cluster,        and handles singleton clusters.\n    '
labeled = np.zeros(shape)
labeled[:, 5:, :] = 1
labeled[4, 2, 6] = 2
labels_index = np.array([1, 1, 2])
ijk = np.array([[4, 7, 5], [4, 2, 5], [4, 3, 6]])
nbrs = _cluster_nearest_neighbor(ijk, labels_index, labeled)
assert np.array_equal(nbrs, np.array([[4, 7, 5], [4, 5, 5], [4, 2, 6]]))
```

## Next Steps


---

*Source: test_get_clusters_table.py:103 | Complexity: Intermediate | Last updated: 2026-05-18*