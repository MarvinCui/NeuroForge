# How To: Cluster Centroid Assign

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster centroid assign

## Prerequisites

**Required Modules:**
- `copy`
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign centroid = np.zeros(...)

```python
centroid = np.zeros(features_shape)
```

**Verification:**
```python
assert_equal(len(cluster), idx)
```

### Step 2: Assign cluster = ClusterCentroid(...)

```python
cluster = ClusterCentroid(centroid)
```

**Verification:**
```python
assert_equal(type(cluster.indices), list)
```

### Step 3: Assign indices = value

```python
indices = []
```

**Verification:**
```python
assert_array_equal(cluster.indices, indices)
```

### Step 4: Assign centroid = np.zeros(...)

```python
centroid = np.zeros(features_shape, dtype=dtype)
```

**Verification:**
```python
assert_equal(type(cluster.centroid), np.ndarray)
```

### Step 5: Call cluster.assign()

```python
cluster.assign(idx, (idx + 1) * features)
```

**Verification:**
```python
assert_array_equal(cluster.centroid, centroid)
```

### Step 6: Call cluster.update()

```python
cluster.update()
```

### Step 7: Call indices.append()

```python
indices.append(idx)
```

### Step 8: Assign centroid = value

```python
centroid = (centroid * (idx - 1) + (idx + 1) * features) / idx
```

### Step 9: Call assert_equal()

```python
assert_equal(len(cluster), idx)
```

### Step 10: Call assert_equal()

```python
assert_equal(type(cluster.indices), list)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(cluster.indices, indices)
```

### Step 12: Call assert_equal()

```python
assert_equal(type(cluster.centroid), np.ndarray)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(cluster.centroid, centroid)
```


## Complete Example

```python
# Workflow
centroid = np.zeros(features_shape)
cluster = ClusterCentroid(centroid)
indices = []
centroid = np.zeros(features_shape, dtype=dtype)
for idx in range(1, 10):
    cluster.assign(idx, (idx + 1) * features)
    cluster.update()
    indices.append(idx)
    centroid = (centroid * (idx - 1) + (idx + 1) * features) / idx
    assert_equal(len(cluster), idx)
    assert_equal(type(cluster.indices), list)
    assert_array_equal(cluster.indices, indices)
    assert_equal(type(cluster.centroid), np.ndarray)
    assert_array_equal(cluster.centroid, centroid)
```

## Next Steps


---

*Source: test_clustering.py:183 | Complexity: Advanced | Last updated: 2026-05-18*