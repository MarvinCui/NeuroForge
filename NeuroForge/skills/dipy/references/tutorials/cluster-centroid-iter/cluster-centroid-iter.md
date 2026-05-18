# How To: Cluster Centroid Iter

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster centroid iter

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign indices = list(...)

```python
indices = list(range(len(data)))
```

**Verification:**
```python
assert_array_equal(cluster.indices, indices)
```

### Step 2: Call rng.shuffle()

```python
rng.shuffle(indices)
```

**Verification:**
```python
assert_array_equal(list(cluster), indices)
```

### Step 3: Assign centroid = np.zeros(...)

```python
centroid = np.zeros(features_shape)
```

**Verification:**
```python
assert_arrays_equal(list(cluster), [data[i] for i in indices])
```

### Step 4: Assign cluster = ClusterCentroid(...)

```python
cluster = ClusterCentroid(centroid)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(cluster.indices, indices)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(list(cluster), indices)
```

### Step 7: Assign cluster.refdata = data

```python
cluster.refdata = data
```

### Step 8: Call assert_arrays_equal()

```python
assert_arrays_equal(list(cluster), [data[i] for i in indices])
```

### Step 9: Call cluster.assign()

```python
cluster.assign(idx, (idx + 1) * features)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
indices = list(range(len(data)))
rng.shuffle(indices)
centroid = np.zeros(features_shape)
cluster = ClusterCentroid(centroid)
for idx in indices:
    cluster.assign(idx, (idx + 1) * features)
assert_array_equal(cluster.indices, indices)
assert_array_equal(list(cluster), indices)
cluster.refdata = data
assert_arrays_equal(list(cluster), [data[i] for i in indices])
```

## Next Steps


---

*Source: test_clustering.py:202 | Complexity: Advanced | Last updated: 2026-05-18*