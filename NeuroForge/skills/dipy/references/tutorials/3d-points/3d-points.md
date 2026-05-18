# How To: 3D Points

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3D points

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign points = np.array(...)

```python
points = np.array([[[1, 0, 0]], [[3, 0, 0]], [[2, 0, 0]], [[5, 0, 0]], [[5.5, 0, 0]]], dtype='f4')
```

**Verification:**
```python
assert_array_equal(clusters_2.clusters_sizes(), [3, 2])
```

### Step 2: Assign thresholds = value

```python
thresholds = [4, 2, 1]
```

**Verification:**
```python
assert_array_equal(clusters_0.clusters_sizes(), [5])
```

### Step 3: Assign metric = AveragePointwiseEuclideanMetric(...)

```python
metric = AveragePointwiseEuclideanMetric()
```

### Step 4: Assign qbx = QuickBundlesX(...)

```python
qbx = QuickBundlesX(thresholds, metric=metric)
```

### Step 5: Assign tree = qbx.cluster(...)

```python
tree = qbx.cluster(points)
```

### Step 6: Assign clusters_2 = tree.get_clusters(...)

```python
clusters_2 = tree.get_clusters(2)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(clusters_2.clusters_sizes(), [3, 2])
```

### Step 8: Assign clusters_0 = tree.get_clusters(...)

```python
clusters_0 = tree.get_clusters(0)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(clusters_0.clusters_sizes(), [5])
```


## Complete Example

```python
# Workflow
points = np.array([[[1, 0, 0]], [[3, 0, 0]], [[2, 0, 0]], [[5, 0, 0]], [[5.5, 0, 0]]], dtype='f4')
thresholds = [4, 2, 1]
metric = AveragePointwiseEuclideanMetric()
qbx = QuickBundlesX(thresholds, metric=metric)
tree = qbx.cluster(points)
clusters_2 = tree.get_clusters(2)
assert_array_equal(clusters_2.clusters_sizes(), [3, 2])
clusters_0 = tree.get_clusters(0)
assert_array_equal(clusters_0.clusters_sizes(), [5])
```

## Next Steps


---

*Source: test_qbx.py:98 | Complexity: Advanced | Last updated: 2026-05-18*