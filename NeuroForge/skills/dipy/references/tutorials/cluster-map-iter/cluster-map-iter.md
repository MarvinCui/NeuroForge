# How To: Cluster Map Iter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map iter

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
assert_true(all((c1 is c2 for c1, c2 in zip(cluster_map.clusters, clusters))))
```

### Step 2: Assign cluster_map = ClusterMap(...)

```python
cluster_map = ClusterMap()
```

**Verification:**
```python
assert_array_equal(cluster_map, clusters)
```

### Step 3: Assign clusters = value

```python
clusters = []
```

**Verification:**
```python
assert_array_equal(cluster_map.clusters, clusters)
```

### Step 4: Call assert_true()

```python
assert_true(all((c1 is c2 for c1, c2 in zip(cluster_map.clusters, clusters))))
```

**Verification:**
```python
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(cluster_map, clusters)
```

**Verification:**
```python
assert_arrays_equal(c1, [data[i] for i in c2.indices])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(cluster_map.clusters, clusters)
```

**Verification:**
```python
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
```

### Step 8: Assign cluster_map.refdata = data

```python
cluster_map.refdata = data
```

### Step 9: Assign cluster_map.refdata = None

```python
cluster_map.refdata = None
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
```

### Step 11: Assign new_cluster = Cluster(...)

```python
new_cluster = Cluster(indices=rng.integers(0, len(data), size=10))
```

### Step 12: Call cluster_map.add_cluster()

```python
cluster_map.add_cluster(new_cluster)
```

### Step 13: Call clusters.append()

```python
clusters.append(new_cluster)
```

### Step 14: Call assert_arrays_equal()

```python
assert_arrays_equal(c1, [data[i] for i in c2.indices])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
nb_clusters = 11
cluster_map = ClusterMap()
clusters = []
for _ in range(nb_clusters):
    new_cluster = Cluster(indices=rng.integers(0, len(data), size=10))
    cluster_map.add_cluster(new_cluster)
    clusters.append(new_cluster)
assert_true(all((c1 is c2 for c1, c2 in zip(cluster_map.clusters, clusters))))
assert_array_equal(cluster_map, clusters)
assert_array_equal(cluster_map.clusters, clusters)
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
cluster_map.refdata = data
for c1, c2 in zip(cluster_map, clusters):
    assert_arrays_equal(c1, [data[i] for i in c2.indices])
cluster_map.refdata = None
assert_array_equal(cluster_map, [cluster.indices for cluster in clusters])
```

## Next Steps


---

*Source: test_clustering.py:377 | Complexity: Advanced | Last updated: 2026-05-18*