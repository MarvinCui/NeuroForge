# How To: Get Clusters Table 4D Image

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Run get_clusters_table on 4D image.

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

### Step 1: 'Run get_clusters_table on 4D image.'

```python
'Run get_clusters_table on 4D image.'
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((*shape, 1))
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

### Step 6: Assign clusters_table = get_clusters_table(...)

```python
clusters_table = get_clusters_table(stat_img, 4, 0, two_sided=True)
```

### Step 7: Call validate_clusters_table()

```python
validate_clusters_table(clusters_table, expected_n_cluster=2)
```


## Complete Example

```python
# Setup
# Fixtures: shape, affine_eye

# Workflow
'Run get_clusters_table on 4D image.'
data = np.zeros((*shape, 1))
data[2:4, 5:7, 6:8] = 5.0
data[4:6, 7:9, 8:10] = -5.0
stat_img = Nifti1Image(data, affine_eye)
clusters_table = get_clusters_table(stat_img, 4, 0, two_sided=True)
validate_clusters_table(clusters_table, expected_n_cluster=2)
```

## Next Steps


---

*Source: test_get_clusters_table.py:395 | Complexity: Intermediate | Last updated: 2026-05-18*