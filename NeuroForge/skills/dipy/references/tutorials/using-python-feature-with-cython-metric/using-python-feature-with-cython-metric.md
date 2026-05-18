# How To: Using Python Feature With Cython Metric

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test using python feature with cython metric

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.segment.featurespeed`
- `dipy.segment.featurespeed`
- `dipy.segment.metric`
- `dipy.segment.metricspeed`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign feature = Identity(...)

```python
feature = Identity()
```

**Verification:**
```python
assert_equal(d1, d2)
```

### Step 2: Assign metric = dipysmetric.AveragePointwiseEuclideanMetric(...)

```python
metric = dipysmetric.AveragePointwiseEuclideanMetric(feature)
```

**Verification:**
```python
assert_equal(d1, d2)
```

### Step 3: Assign d1 = dipymetric.dist(...)

```python
d1 = dipymetric.dist(metric, s1, s2)
```

### Step 4: Assign features1 = metric.feature.extract(...)

```python
features1 = metric.feature.extract(s1)
```

### Step 5: Assign features2 = metric.feature.extract(...)

```python
features2 = metric.feature.extract(s2)
```

### Step 6: Assign d2 = metric.dist(...)

```python
d2 = metric.dist(features1, features2)
```

### Step 7: Call assert_equal()

```python
assert_equal(d1, d2)
```

### Step 8: Assign feature = ArcLengthFeature(...)

```python
feature = ArcLengthFeature()
```

### Step 9: Assign metric = dipymetric.EuclideanMetric(...)

```python
metric = dipymetric.EuclideanMetric(feature)
```

### Step 10: Assign d1 = dipymetric.dist(...)

```python
d1 = dipymetric.dist(metric, s1, s2)
```

### Step 11: Assign features1 = metric.feature.extract(...)

```python
features1 = metric.feature.extract(s1)
```

### Step 12: Assign features2 = metric.feature.extract(...)

```python
features2 = metric.feature.extract(s2)
```

### Step 13: Assign d2 = metric.dist(...)

```python
d2 = metric.dist(features1, features2)
```

### Step 14: Call assert_equal()

```python
assert_equal(d1, d2)
```

### Step 15: Assign square_norms = np.sum(...)

```python
square_norms = np.sum((streamline[1:] - streamline[:-1]) ** 2)
```


## Complete Example

```python
# Workflow
class Identity(dipysfeature.Feature):

    def infer_shape(self, streamline):
        return streamline.shape

    def extract(self, streamline):
        return streamline
feature = Identity()
metric = dipysmetric.AveragePointwiseEuclideanMetric(feature)
d1 = dipymetric.dist(metric, s1, s2)
features1 = metric.feature.extract(s1)
features2 = metric.feature.extract(s2)
d2 = metric.dist(features1, features2)
assert_equal(d1, d2)

class ArcLengthFeature(dipysfeature.Feature):

    def infer_shape(self, streamline):
        return 1

    def extract(self, streamline):
        square_norms = np.sum((streamline[1:] - streamline[:-1]) ** 2)
        return np.sum(np.sqrt(square_norms))
feature = ArcLengthFeature()
metric = dipymetric.EuclideanMetric(feature)
d1 = dipymetric.dist(metric, s1, s2)
features1 = metric.feature.extract(s1)
features2 = metric.feature.extract(s2)
d2 = metric.dist(features1, features2)
assert_equal(d1, d2)
```

## Next Steps


---

*Source: test_feature.py:291 | Complexity: Advanced | Last updated: 2026-05-18*