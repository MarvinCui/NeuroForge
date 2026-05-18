# How To: Feature Vector Of Endpoints

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test feature vector of endpoints

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

### Step 1: Assign feature_types = value

```python
feature_types = [dipysfeature.VectorOfEndpointsFeature(), VectorOfEndpointsFeature()]
```

**Verification:**
```python
assert_equal(feature.infer_shape(s), (1, s.shape[1]))
```

### Step 2: Call assert_false()

```python
assert_false(feature.is_order_invariant)
```

**Verification:**
```python
assert_equal(features.shape, (1, s.shape[1]))
```

### Step 3: Call super.__init__()

```python
super().__init__(False)
```

**Verification:**
```python
assert_array_almost_equal(features, s[[-1]] - s[[0]])
```

### Step 4: Call assert_equal()

```python
assert_equal(feature.infer_shape(s), (1, s.shape[1]))
```

**Verification:**
```python
assert_false(feature.is_order_invariant)
```

### Step 5: Assign features = feature.extract(...)

```python
features = feature.extract(s)
```

**Verification:**
```python
assert_array_almost_equal(features, -features_flip)
```

### Step 6: Call assert_equal()

```python
assert_equal(features.shape, (1, s.shape[1]))
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(features, s[[-1]] - s[[0]])
```

### Step 8: Assign features = feature.extract(...)

```python
features = feature.extract(s)
```

### Step 9: Assign features_flip = feature.extract(...)

```python
features_flip = feature.extract(s[::-1])
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(features, -features_flip)
```


## Complete Example

```python
# Workflow
class VectorOfEndpointsFeature(dipysfeature.Feature):

    def __init__(self):
        super().__init__(False)

    def infer_shape(self, streamline):
        return (1, streamline.shape[1])

    def extract(self, streamline):
        return streamline[[-1]] - streamline[[0]]
feature_types = [dipysfeature.VectorOfEndpointsFeature(), VectorOfEndpointsFeature()]
for feature in feature_types:
    for s in [s1, s2, s3, s4]:
        assert_equal(feature.infer_shape(s), (1, s.shape[1]))
        features = feature.extract(s)
        assert_equal(features.shape, (1, s.shape[1]))
        assert_array_almost_equal(features, s[[-1]] - s[[0]])
    assert_false(feature.is_order_invariant)
    for s in [s1, s2, s3, s4]:
        features = feature.extract(s)
        features_flip = feature.extract(s[::-1])
        assert_array_almost_equal(features, -features_flip)
```

## Next Steps


---

*Source: test_feature.py:202 | Complexity: Advanced | Last updated: 2026-05-18*