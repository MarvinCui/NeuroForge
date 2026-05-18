# How To: Quickbundles With Python Metric

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quickbundles with python metric

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

### Step 1: Assign rdata = streamline_utils.set_number_of_points(...)

```python
rdata = streamline_utils.set_number_of_points(data, nb_points=10)
```

**Verification:**
```python
assert_equal(clusters.refdata, rdata)
```

### Step 2: Assign qb = QuickBundles(...)

```python
qb = QuickBundles(threshold=2 * threshold, metric=MDFpy())
```

**Verification:**
```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*clusters_truth)))
```

### Step 3: Assign clusters = qb.cluster(...)

```python
clusters = qb.cluster(rdata)
```

**Verification:**
```python
assert_equal(clusters.centroids[0].dtype, np.float32)
```

### Step 4: Call assert_equal()

```python
assert_equal(clusters.refdata, rdata)
```

### Step 5: Assign clusters.refdata = None

```python
clusters.refdata = None
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*clusters_truth)))
```

### Step 7: Call datum.setflags()

```python
datum.setflags(write=False)
```

### Step 8: Assign newdata = value

```python
newdata = [datum.astype(datatype) for datum in rdata]
```

### Step 9: Assign clusters = qb.cluster(...)

```python
clusters = qb.cluster(newdata)
```

### Step 10: Call assert_equal()

```python
assert_equal(clusters.centroids[0].dtype, np.float32)
```

### Step 11: Assign dist = np.sqrt(...)

```python
dist = np.sqrt(np.sum((features1 - features2) ** 2, axis=1))
```

### Step 12: Assign dist = np.sum(...)

```python
dist = np.sum(dist / len(features1))
```


## Complete Example

```python
# Workflow
class MDFpy(dipysmetric.Metric):

    def are_compatible(self, shape1, shape2):
        return shape1 == shape2

    def dist(self, features1, features2):
        dist = np.sqrt(np.sum((features1 - features2) ** 2, axis=1))
        dist = np.sum(dist / len(features1))
        return dist
rdata = streamline_utils.set_number_of_points(data, nb_points=10)
qb = QuickBundles(threshold=2 * threshold, metric=MDFpy())
clusters = qb.cluster(rdata)
assert_equal(clusters.refdata, rdata)
clusters.refdata = None
assert_array_equal(list(itertools.chain(*clusters)), list(itertools.chain(*clusters_truth)))
for datum in rdata:
    datum.setflags(write=False)
for datatype in [np.float64, np.int32, np.int64]:
    newdata = [datum.astype(datatype) for datum in rdata]
    clusters = qb.cluster(newdata)
    assert_equal(clusters.centroids[0].dtype, np.float32)
```

## Next Steps


---

*Source: test_quickbundles.py:150 | Complexity: Advanced | Last updated: 2026-05-18*