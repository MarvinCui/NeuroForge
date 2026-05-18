# How To: Local Max Donut

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Basic test of nilearn.reporting._get_clusters_table._local_max().

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

### Step 1: 'Basic test of nilearn.reporting._get_clusters_table._local_max().'

```python
'Basic test of nilearn.reporting._get_clusters_table._local_max().'
```

**Verification:**
```python
assert np.array_equal(ijk, np.array([[4.0, 5.0, 5.0]]))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros(shape)
```

**Verification:**
```python
assert np.array_equal(vals, np.array([1]))
```

### Step 3: Assign unknown = value

```python
data[4, 5, :] = [0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0]
```

### Step 4: Assign unknown = value

```python
data[5, 5, :] = [0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0]
```

### Step 5: Assign unknown = value

```python
data[6, 5, :] = [0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0]
```

**Verification:**
```python
assert np.array_equal(ijk, np.array([[4.0, 5.0, 5.0]]))
```

### Step 6: Assign unknown = _local_max(...)

```python
ijk, vals = _local_max(data, affine_eye, min_distance=9)
```


## Complete Example

```python
# Setup
# Fixtures: shape, affine_eye

# Workflow
'Basic test of nilearn.reporting._get_clusters_table._local_max().'
data = np.zeros(shape)
data[4, 5, :] = [0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0]
data[5, 5, :] = [0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0]
data[6, 5, :] = [0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0]
with pytest.warns(UserWarning, match='falls outside of the cluster body.'):
    ijk, vals = _local_max(data, affine_eye, min_distance=9)
assert np.array_equal(ijk, np.array([[4.0, 5.0, 5.0]]))
assert np.array_equal(vals, np.array([1]))
```

## Next Steps


---

*Source: test_get_clusters_table.py:89 | Complexity: Intermediate | Last updated: 2026-05-18*