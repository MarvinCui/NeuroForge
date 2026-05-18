# How To: Cluster Map Str And Repr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map str and repr

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

### Step 1: Assign nb_clusters = 11

```python
nb_clusters = 11
```

**Verification:**
```python
assert_equal(str(cluster_map), expected_str)
```

### Step 2: Assign cluster_map = ClusterMap(...)

```python
cluster_map = ClusterMap()
```

**Verification:**
```python
assert_equal(repr(cluster_map), f'ClusterMap({expected_str})')
```

### Step 3: Assign clusters = value

```python
clusters = []
```

### Step 4: Assign expected_str = value

```python
expected_str = '[' + ', '.join(map(str, clusters)) + ']'
```

### Step 5: Call assert_equal()

```python
assert_equal(str(cluster_map), expected_str)
```

### Step 6: Call assert_equal()

```python
assert_equal(repr(cluster_map), f'ClusterMap({expected_str})')
```

### Step 7: Assign new_cluster = Cluster(...)

```python
new_cluster = Cluster(indices=range(i))
```

### Step 8: Call cluster_map.add_cluster()

```python
cluster_map.add_cluster(new_cluster)
```

### Step 9: Call clusters.append()

```python
clusters.append(new_cluster)
```


## Complete Example

```python
# Workflow
nb_clusters = 11
cluster_map = ClusterMap()
clusters = []
for i in range(nb_clusters):
    new_cluster = Cluster(indices=range(i))
    cluster_map.add_cluster(new_cluster)
    clusters.append(new_cluster)
expected_str = '[' + ', '.join(map(str, clusters)) + ']'
assert_equal(str(cluster_map), expected_str)
assert_equal(repr(cluster_map), f'ClusterMap({expected_str})')
```

## Next Steps


---

*Source: test_clustering.py:440 | Complexity: Advanced | Last updated: 2026-05-18*