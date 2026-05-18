# How To: Cluster Map Remove Cluster

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster map remove cluster

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
assert_equal(len(clusters), 3)
```

### Step 2: Assign cluster1 = Cluster(...)

```python
cluster1 = Cluster(indices=[1])
```

**Verification:**
```python
assert_equal(len(clusters), 2)
```

### Step 3: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster1)
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*[cluster1, cluster3])))
```

### Step 4: Assign cluster2 = Cluster(...)

```python
cluster2 = Cluster(indices=[1, 2])
```

**Verification:**
```python
assert_equal(clusters[0], cluster1)
```

### Step 5: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster2)
```

**Verification:**
```python
assert_equal(clusters[1], cluster3)
```

### Step 6: Assign cluster3 = Cluster(...)

```python
cluster3 = Cluster(indices=[1, 2, 3])
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 7: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster3)
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
```

### Step 8: Call assert_equal()

```python
assert_equal(len(clusters), 3)
```

**Verification:**
```python
assert_equal(clusters[0], cluster1)
```

### Step 9: Call clusters.remove_cluster()

```python
clusters.remove_cluster(cluster2)
```

**Verification:**
```python
assert_equal(len(clusters), 0)
```

### Step 10: Call assert_equal()

```python
assert_equal(len(clusters), 2)
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), [])
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*[cluster1, cluster3])))
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 12: Call assert_equal()

```python
assert_equal(clusters[0], cluster1)
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
```

### Step 13: Call assert_equal()

```python
assert_equal(clusters[1], cluster3)
```

**Verification:**
```python
assert_equal(clusters[0], cluster1)
```

### Step 14: Call clusters.remove_cluster()

```python
clusters.remove_cluster(cluster3)
```

**Verification:**
```python
assert_equal(len(clusters), 0)
```

### Step 15: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), [])
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
```

### Step 17: Call assert_equal()

```python
assert_equal(clusters[0], cluster1)
```

### Step 18: Call clusters.remove_cluster()

```python
clusters.remove_cluster(cluster1)
```

### Step 19: Call assert_equal()

```python
assert_equal(len(clusters), 0)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), [])
```

### Step 21: Assign clusters = ClusterMap(...)

```python
clusters = ClusterMap()
```

### Step 22: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster1, cluster2, cluster3)
```

### Step 23: Call clusters.remove_cluster()

```python
clusters.remove_cluster(cluster3, cluster2)
```

### Step 24: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

### Step 25: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
```

### Step 26: Call assert_equal()

```python
assert_equal(clusters[0], cluster1)
```

### Step 27: Assign clusters = ClusterMap(...)

```python
clusters = ClusterMap()
```

### Step 28: Call clusters.add_cluster()

```python
clusters.add_cluster(cluster2, cluster1, cluster3)
```

### Step 29: Call clusters.remove_cluster()

```python
clusters.remove_cluster(cluster1, cluster3, cluster2)
```

### Step 30: Call assert_equal()

```python
assert_equal(len(clusters), 0)
```

### Step 31: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), [])
```


## Complete Example

```python
# Workflow
clusters = ClusterMap()
cluster1 = Cluster(indices=[1])
clusters.add_cluster(cluster1)
cluster2 = Cluster(indices=[1, 2])
clusters.add_cluster(cluster2)
cluster3 = Cluster(indices=[1, 2, 3])
clusters.add_cluster(cluster3)
assert_equal(len(clusters), 3)
clusters.remove_cluster(cluster2)
assert_equal(len(clusters), 2)
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*[cluster1, cluster3])))
assert_equal(clusters[0], cluster1)
assert_equal(clusters[1], cluster3)
clusters.remove_cluster(cluster3)
assert_equal(len(clusters), 1)
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
assert_equal(clusters[0], cluster1)
clusters.remove_cluster(cluster1)
assert_equal(len(clusters), 0)
assert_array_equal(list(itertools.chain(*clusters)), [])
clusters = ClusterMap()
clusters.add_cluster(cluster1, cluster2, cluster3)
clusters.remove_cluster(cluster3, cluster2)
assert_equal(len(clusters), 1)
assert_array_equal(list(itertools.chain(*clusters)), list(cluster1))
assert_equal(clusters[0], cluster1)
clusters = ClusterMap()
clusters.add_cluster(cluster2, cluster1, cluster3)
clusters.remove_cluster(cluster1, cluster3, cluster2)
assert_equal(len(clusters), 0)
assert_array_equal(list(itertools.chain(*clusters)), [])
```

## Next Steps


---

*Source: test_clustering.py:316 | Complexity: Advanced | Last updated: 2026-05-18*