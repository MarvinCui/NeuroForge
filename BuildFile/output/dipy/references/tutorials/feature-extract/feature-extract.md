# How To: Feature Extract

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test feature extract

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign nb_streamlines = 100

```python
nb_streamlines = 100
```

**Verification:**
```python
assert_equal(len(features), len(streamlines))
```

### Step 2: Assign feature_shape = value

```python
feature_shape = (1, 3)
```

**Verification:**
```python
assert_equal(features[0].shape, feature_shape)
```

### Step 3: Assign feature = CenterOfMass64bit(...)

```python
feature = CenterOfMass64bit()
```

**Verification:**
```python
assert_equal(len(features), len(streamlines))
```

### Step 4: Assign nb_points = value

```python
nb_points = rng.integers(20, 30, size=(nb_streamlines,)) * 3
```

**Verification:**
```python
assert_equal(features[0].shape, feature_shape)
```

### Step 5: Assign streamlines = value

```python
streamlines = [np.arange(nb).reshape((-1, 3)).astype(np.float32) for nb in nb_points]
```

### Step 6: Assign features = extract(...)

```python
features = extract(feature, streamlines)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(features), len(streamlines))
```

### Step 8: Call assert_equal()

```python
assert_equal(features[0].shape, feature_shape)
```

### Step 9: Assign feature_shape = value

```python
feature_shape = (1, 1)
```

### Step 10: Assign feature = ArcLengthFeature(...)

```python
feature = ArcLengthFeature()
```

### Step 11: Assign features = extract(...)

```python
features = extract(feature, streamlines)
```

### Step 12: Call assert_equal()

```python
assert_equal(len(features), len(streamlines))
```

### Step 13: Call assert_equal()

```python
assert_equal(features[0].shape, feature_shape)
```

### Step 14: Call s.setflags()

```python
s.setflags(write=False)
```

### Step 15: Assign square_norms = np.sum(...)

```python
square_norms = np.sum((streamline[1:] - streamline[:-1]) ** 2)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
class CenterOfMass64bit(dipysfeature.Feature):

    def infer_shape(self, streamline):
        return streamline.shape[1]

    def extract(self, streamline):
        return np.mean(streamline.astype(np.float64), axis=0)
nb_streamlines = 100
feature_shape = (1, 3)
feature = CenterOfMass64bit()
nb_points = rng.integers(20, 30, size=(nb_streamlines,)) * 3
streamlines = [np.arange(nb).reshape((-1, 3)).astype(np.float32) for nb in nb_points]
features = extract(feature, streamlines)
assert_equal(len(features), len(streamlines))
assert_equal(features[0].shape, feature_shape)

class ArcLengthFeature(dipysfeature.Feature):

    def infer_shape(self, streamline):
        return 1

    def extract(self, streamline):
        square_norms = np.sum((streamline[1:] - streamline[:-1]) ** 2)
        return np.sum(np.sqrt(square_norms))
feature_shape = (1, 1)
feature = ArcLengthFeature()
features = extract(feature, streamlines)
assert_equal(len(features), len(streamlines))
assert_equal(features[0].shape, feature_shape)
for s in streamlines:
    s.setflags(write=False)
```

## Next Steps


---

*Source: test_feature.py:238 | Complexity: Advanced | Last updated: 2026-05-18*