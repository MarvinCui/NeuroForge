# How To: Cluster Map Getitem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map getitem

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

### Step 1: Assign nb_clusters = 11

```python
nb_clusters = 11
```

**Verification:**
```python
assert_true(cluster_map[i] == clusters[i])
```

### Step 2: Assign indices = list(...)

```python
indices = list(range(nb_clusters))
```

**Verification:**
```python
assert_arrays_equal(cluster_map[advanced_indices], [clusters[i] for i in advanced_indices])
```

### Step 3: Call rng.shuffle()

```python
rng.shuffle(indices)
```

**Verification:**
```python
assert_raises(IndexError, cluster_map.__getitem__, len(clusters))
```

### Step 4: Assign advanced_indices = value

```python
advanced_indices = indices + [0, 1, 2, -1, -2, -3]
```

**Verification:**
```python
assert_raises(IndexError, cluster_map.__getitem__, -len(clusters) - 1)
```

### Step 5: Assign cluster_map = ClusterMap(...)

```python
cluster_map = ClusterMap()
```

**Verification:**
```python
assert_equal(cluster_map[-1], clusters[-1])
```

### Step 6: Assign clusters = value

```python
clusters = []
```

**Verification:**
```python
assert_array_equal(np.array(cluster_map[::2], dtype=object), np.array(clusters[::2], dtype=object))
```

### Step 7: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster_map[advanced_indices], [clusters[i] for i in advanced_indices])
```

**Verification:**
```python
assert_arrays_equal(cluster_map[::-1], clusters[::-1])
```

### Step 8: Call assert_raises()

```python
assert_raises(IndexError, cluster_map.__getitem__, len(clusters))
```

**Verification:**
```python
assert_arrays_equal(cluster_map[:-1], clusters[:-1])
```

### Step 9: Call assert_raises()

```python
assert_raises(IndexError, cluster_map.__getitem__, -len(clusters) - 1)
```

**Verification:**
```python
assert_arrays_equal(cluster_map[1:], clusters[1:])
```

### Step 10: Call assert_equal()

```python
assert_equal(cluster_map[-1], clusters[-1])
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(np.array(cluster_map[::2], dtype=object), np.array(clusters[::2], dtype=object))
```

### Step 12: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster_map[::-1], clusters[::-1])
```

### Step 13: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster_map[:-1], clusters[:-1])
```

### Step 14: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster_map[1:], clusters[1:])
```

### Step 15: Assign new_cluster = Cluster(...)

```python
new_cluster = Cluster(indices=range(i))
```

### Step 16: Call cluster_map.add_cluster()

```python
cluster_map.add_cluster(new_cluster)
```

### Step 17: Call clusters.append()

```python
clusters.append(new_cluster)
```

### Step 18: Call assert_true()

```python
assert_true(cluster_map[i] == clusters[i])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
nb_clusters = 11
indices = list(range(nb_clusters))
rng.shuffle(indices)
advanced_indices = indices + [0, 1, 2, -1, -2, -3]
cluster_map = ClusterMap()
clusters = []
for i in range(nb_clusters):
    new_cluster = Cluster(indices=range(i))
    cluster_map.add_cluster(new_cluster)
    clusters.append(new_cluster)
for i in advanced_indices:
    assert_true(cluster_map[i] == clusters[i])
assert_arrays_equal(cluster_map[advanced_indices], [clusters[i] for i in advanced_indices])
assert_raises(IndexError, cluster_map.__getitem__, len(clusters))
assert_raises(IndexError, cluster_map.__getitem__, -len(clusters) - 1)
assert_equal(cluster_map[-1], clusters[-1])
assert_array_equal(np.array(cluster_map[::2], dtype=object), np.array(clusters[::2], dtype=object))
assert_arrays_equal(cluster_map[::-1], clusters[::-1])
assert_arrays_equal(cluster_map[:-1], clusters[:-1])
assert_arrays_equal(cluster_map[1:], clusters[1:])
```

## Next Steps


---

*Source: test_clustering.py:404 | Complexity: Advanced | Last updated: 2026-05-18*