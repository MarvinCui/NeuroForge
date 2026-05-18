# How To: Cluster Map Clusters Sizes

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map clusters sizes

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
assert_equal(cluster_map.clusters_sizes(), list(map(len, indices)))
```

### Step 2: Assign indices = value

```python
indices = [range(rng.integers(1, 10)) for _ in range(nb_clusters)]
```

### Step 3: Assign cluster_map = ClusterMap(...)

```python
cluster_map = ClusterMap()
```

### Step 4: Assign clusters = value

```python
clusters = [Cluster(indices=indices[i]) for i in range(nb_clusters)]
```

### Step 5: Call cluster_map.add_cluster()

```python
cluster_map.add_cluster(*clusters)
```

### Step 6: Call assert_equal()

```python
assert_equal(cluster_map.clusters_sizes(), list(map(len, indices)))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
nb_clusters = 11
indices = [range(rng.integers(1, 10)) for _ in range(nb_clusters)]
cluster_map = ClusterMap()
clusters = [Cluster(indices=indices[i]) for i in range(nb_clusters)]
cluster_map.add_cluster(*clusters)
assert_equal(cluster_map.clusters_sizes(), list(map(len, indices)))
```

## Next Steps


---

*Source: test_clustering.py:465 | Complexity: Intermediate | Last updated: 2026-05-18*