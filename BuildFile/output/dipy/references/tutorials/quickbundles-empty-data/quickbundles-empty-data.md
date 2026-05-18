# How To: Quickbundles Empty Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quickbundles empty data

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

### Step 1: Assign threshold = 10

```python
threshold = 10
```

**Verification:**
```python
assert_equal(len(clusters), 0)
```

### Step 2: Assign metric = dipysmetric.SumPointwiseEuclideanMetric(...)

```python
metric = dipysmetric.SumPointwiseEuclideanMetric()
```

**Verification:**
```python
assert_equal(len(clusters.centroids), 0)
```

### Step 3: Assign clusters = quickbundles(...)

```python
clusters = quickbundles([], metric, threshold)
```

**Verification:**
```python
assert_equal(len(clusters), 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(len(clusters), 0)
```

**Verification:**
```python
assert_equal(len(clusters.centroids), 0)
```

### Step 5: Call assert_equal()

```python
assert_equal(len(clusters.centroids), 0)
```

### Step 6: Assign clusters = quickbundles(...)

```python
clusters = quickbundles([], metric, threshold, ordering=[])
```

### Step 7: Call assert_equal()

```python
assert_equal(len(clusters), 0)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(clusters.centroids), 0)
```


## Complete Example

```python
# Workflow
threshold = 10
metric = dipysmetric.SumPointwiseEuclideanMetric()
clusters = quickbundles([], metric, threshold)
assert_equal(len(clusters), 0)
assert_equal(len(clusters.centroids), 0)
clusters = quickbundles([], metric, threshold, ordering=[])
assert_equal(len(clusters), 0)
assert_equal(len(clusters.centroids), 0)
```

## Next Steps


---

*Source: test_quickbundles.py:28 | Complexity: Advanced | Last updated: 2026-05-18*