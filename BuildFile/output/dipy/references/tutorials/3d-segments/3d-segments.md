# How To: 3D Segments

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3D segments

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
points = np.array([[[1, 0, 0], [1, 1, 0]], [[3, 1, 0], [3, 0, 0]], [[2, 0, 0], [2, 1, 0]], [[5, 1, 0], [5, 0, 0]], [[5.5, 0, 0], [5.5, 1, 0]]], dtype='f4')
```

**Verification:**
```python
assert_equal(len(clusters_0.centroids), len(clusters_1.centroids))
```

### Step 2: Assign thresholds = value

```python
thresholds = [4, 2, 1]
```

**Verification:**
```python
assert_equal(len(clusters_2.centroids) > len(clusters_1.centroids), True)
```

### Step 3: Assign feature = ResampleFeature(...)

```python
feature = ResampleFeature(nb_points=20)
```

**Verification:**
```python
assert_array_equal(clusters_2[1].indices, np.array([3, 4], dtype=np.int32))
```

### Step 4: Assign metric = AveragePointwiseEuclideanMetric(...)

```python
metric = AveragePointwiseEuclideanMetric(feature)
```

### Step 5: Assign qbx = QuickBundlesX(...)

```python
qbx = QuickBundlesX(thresholds, metric=metric)
```

### Step 6: Assign tree = qbx.cluster(...)

```python
tree = qbx.cluster(points)
```

### Step 7: Assign clusters_0 = tree.get_clusters(...)

```python
clusters_0 = tree.get_clusters(0)
```

### Step 8: Assign clusters_1 = tree.get_clusters(...)

```python
clusters_1 = tree.get_clusters(1)
```

### Step 9: Assign clusters_2 = tree.get_clusters(...)

```python
clusters_2 = tree.get_clusters(2)
```

### Step 10: Call assert_equal()

```python
assert_equal(len(clusters_0.centroids), len(clusters_1.centroids))
```

### Step 11: Call assert_equal()

```python
assert_equal(len(clusters_2.centroids) > len(clusters_1.centroids), True)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(clusters_2[1].indices, np.array([3, 4], dtype=np.int32))
```


## Complete Example

```python
# Workflow
points = np.array([[[1, 0, 0], [1, 1, 0]], [[3, 1, 0], [3, 0, 0]], [[2, 0, 0], [2, 1, 0]], [[5, 1, 0], [5, 0, 0]], [[5.5, 0, 0], [5.5, 1, 0]]], dtype='f4')
thresholds = [4, 2, 1]
feature = ResampleFeature(nb_points=20)
metric = AveragePointwiseEuclideanMetric(feature)
qbx = QuickBundlesX(thresholds, metric=metric)
tree = qbx.cluster(points)
clusters_0 = tree.get_clusters(0)
clusters_1 = tree.get_clusters(1)
clusters_2 = tree.get_clusters(2)
assert_equal(len(clusters_0.centroids), len(clusters_1.centroids))
assert_equal(len(clusters_2.centroids) > len(clusters_1.centroids), True)
assert_array_equal(clusters_2[1].indices, np.array([3, 4], dtype=np.int32))
```

## Next Steps


---

*Source: test_qbx.py:113 | Complexity: Advanced | Last updated: 2026-05-18*