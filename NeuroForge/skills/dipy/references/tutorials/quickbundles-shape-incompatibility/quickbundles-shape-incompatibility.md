# How To: Quickbundles Shape Incompatibility

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quickbundles shape incompatibility

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
assert_raises(ValueError, qb.cluster, data)
```

### Step 2: Assign qb = QuickBundles(...)

```python
qb = QuickBundles(threshold=20.0, metric=metric)
```

**Verification:**
```python
assert_arrays_equal(list(itertools.chain(*clusters1)), list(itertools.chain(*clusters2)))
```

### Step 3: Call assert_raises()

```python
assert_raises(ValueError, qb.cluster, data)
```

### Step 4: Assign qb = QuickBundles(...)

```python
qb = QuickBundles(threshold=20.0)
```

### Step 5: Assign clusters1 = qb.cluster(...)

```python
clusters1 = qb.cluster(data)
```

### Step 6: Assign feature = dipysfeature.ResampleFeature(...)

```python
feature = dipysfeature.ResampleFeature(nb_points=18)
```

### Step 7: Assign metric = dipysmetric.AveragePointwiseEuclideanMetric(...)

```python
metric = dipysmetric.AveragePointwiseEuclideanMetric(feature)
```

### Step 8: Assign qb = QuickBundles(...)

```python
qb = QuickBundles(threshold=20.0, metric=metric)
```

### Step 9: Assign clusters2 = qb.cluster(...)

```python
clusters2 = qb.cluster(data)
```

### Step 10: Call assert_arrays_equal()

```python
assert_arrays_equal(list(itertools.chain(*clusters1)), list(itertools.chain(*clusters2)))
```


## Complete Example

```python
# Workflow
metric = dipysmetric.AveragePointwiseEuclideanMetric()
qb = QuickBundles(threshold=20.0, metric=metric)
assert_raises(ValueError, qb.cluster, data)
qb = QuickBundles(threshold=20.0)
clusters1 = qb.cluster(data)
feature = dipysfeature.ResampleFeature(nb_points=18)
metric = dipysmetric.AveragePointwiseEuclideanMetric(feature)
qb = QuickBundles(threshold=20.0, metric=metric)
clusters2 = qb.cluster(data)
assert_arrays_equal(list(itertools.chain(*clusters1)), list(itertools.chain(*clusters2)))
```

## Next Steps


---

*Source: test_quickbundles.py:44 | Complexity: Advanced | Last updated: 2026-05-18*