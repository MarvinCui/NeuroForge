# How To: Local Max Two Maxima

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
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
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0], [5.0, 5.0, 0.0]]))
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros(shape)
```

**Verification:**
```python
assert np.array_equal(vals, np.array([6, 5]))
```

### Step 3: Assign unknown = value

```python
data[4, 5, :] = [4, 3, 2, 1, 1, 1, 1, 1, 2, 3, 4]
```

**Verification:**
```python
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0]]))
```

### Step 4: Assign unknown = value

```python
data[5, 5, :] = [5, 4, 3, 2, 1, 1, 1, 2, 3, 4, 6]
```

**Verification:**
```python
assert np.array_equal(vals, np.array([6]))
```

### Step 5: Assign unknown = value

```python
data[6, 5, :] = [4, 3, 2, 1, 1, 1, 1, 1, 2, 3, 4]
```

### Step 6: Assign unknown = _local_max(...)

```python
ijk, vals = _local_max(data, affine_eye, min_distance=9)
```

**Verification:**
```python
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0], [5.0, 5.0, 0.0]]))
```

### Step 7: Assign unknown = _local_max(...)

```python
ijk, vals = _local_max(data, affine_eye, min_distance=11)
```

**Verification:**
```python
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0]]))
```


## Complete Example

```python
# Setup
# Fixtures: shape, affine_eye

# Workflow
'Basic test of nilearn.reporting._get_clusters_table._local_max().'
data = np.zeros(shape)
data[4, 5, :] = [4, 3, 2, 1, 1, 1, 1, 1, 2, 3, 4]
data[5, 5, :] = [5, 4, 3, 2, 1, 1, 1, 2, 3, 4, 6]
data[6, 5, :] = [4, 3, 2, 1, 1, 1, 1, 1, 2, 3, 4]
ijk, vals = _local_max(data, affine_eye, min_distance=9)
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0], [5.0, 5.0, 0.0]]))
assert np.array_equal(vals, np.array([6, 5]))
ijk, vals = _local_max(data, affine_eye, min_distance=11)
assert np.array_equal(ijk, np.array([[5.0, 5.0, 10.0]]))
assert np.array_equal(vals, np.array([6]))
```

## Next Steps


---

*Source: test_get_clusters_table.py:55 | Complexity: Intermediate | Last updated: 2026-05-18*