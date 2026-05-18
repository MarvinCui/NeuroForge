# How To: Quickbundles With Not Order Invariant Metric

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quickbundles with not order invariant metric

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.clustering_algorithms`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign metric = dipysmetric.AveragePointwiseEuclideanMetric(...)

```python
metric = dipysmetric.AveragePointwiseEuclideanMetric()
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 2: Assign qb = QuickBundles(...)

```python
qb = QuickBundles(threshold=np.inf, metric=metric)
```

**Verification:**
```python
assert_array_equal(clusters[0].centroid, streamline)
```

### Step 3: Assign streamline = np.arange.reshape(...)

```python
streamline = np.arange(10 * 3, dtype=dtype).reshape((-1, 3))
```

### Step 4: Assign streamlines = value

```python
streamlines = [streamline, streamline[::-1]]
```

### Step 5: Assign clusters = qb.cluster(...)

```python
clusters = qb.cluster(streamlines)
```

### Step 6: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(clusters[0].centroid, streamline)
```


## Complete Example

```python
# Workflow
metric = dipysmetric.AveragePointwiseEuclideanMetric()
qb = QuickBundles(threshold=np.inf, metric=metric)
streamline = np.arange(10 * 3, dtype=dtype).reshape((-1, 3))
streamlines = [streamline, streamline[::-1]]
clusters = qb.cluster(streamlines)
assert_equal(len(clusters), 1)
assert_array_equal(clusters[0].centroid, streamline)
```

## Next Steps


---

*Source: test_quickbundles.py:184 | Complexity: Intermediate | Last updated: 2026-05-18*