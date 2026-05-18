# How To: Cluster Map Add Cluster

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map add cluster

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

### Step 1: Assign clusters = ClusterMap(...)

```python
clusters = ClusterMap()
```

**Verification:**
```python
assert_equal(type(cluster), Cluster)
```

### Step 2: Assign list_of_cluster_objects = value

```python
list_of_cluster_objects = []
```

**Verification:**
```python
assert_equal(len(clusters), i + 1)
```

### Step 3: Assign list_of_indices = value

```python
list_of_indices = []
```

**Verification:**
```python
assert_true(cluster == clusters[-1])
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
```

### Step 5: Assign clusters = ClusterMap(...)

```python
clusters = ClusterMap()
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
```

### Step 6: Call clusters.add_cluster()

```python
clusters.add_cluster(*list_of_cluster_objects)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
```

### Step 8: Assign cluster = Cluster(...)

```python
cluster = Cluster()
```

### Step 9: Call list_of_cluster_objects.append()

```python
list_of_cluster_objects.append(cluster)
```

### Step 10: Call list_of_indices.append()

```python
list_of_indices.append([])
```

### Step 11: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster)
```

### Step 12: Call assert_equal()

```python
assert_equal(type(cluster), Cluster)
```

### Step 13: Call assert_equal()

```python
assert_equal(len(clusters), i + 1)
```

### Step 14: Call assert_true()

```python
assert_true(cluster == clusters[-1])
```

### Step 15: Call unknown.append()

```python
list_of_indices[-1].append(id_data)
```

### Step 16: Call cluster.assign()

```python
cluster.assign(id_data)
```


## Complete Example

```python
# Workflow
clusters = ClusterMap()
list_of_cluster_objects = []
list_of_indices = []
for i in range(3):
    cluster = Cluster()
    list_of_cluster_objects.append(cluster)
    list_of_indices.append([])
    for id_data in range(2 * i):
        list_of_indices[-1].append(id_data)
        cluster.assign(id_data)
    clusters.add_cluster(cluster)
    assert_equal(type(cluster), Cluster)
    assert_equal(len(clusters), i + 1)
    assert_true(cluster == clusters[-1])
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
clusters = ClusterMap()
clusters.add_cluster(*list_of_cluster_objects)
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*list_of_indices)))
```

## Next Steps


---

*Source: test_clustering.py:285 | Complexity: Advanced | Last updated: 2026-05-18*