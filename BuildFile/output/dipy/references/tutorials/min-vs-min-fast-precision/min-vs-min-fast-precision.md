# How To: Min Vs Min Fast Precision

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test min vs min fast precision

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.bundlemin`
- `dipy.align.streamlinear`
- `dipy.core.geometry`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign static = value

```python
static = fornix_streamlines()[:20]
```

**Verification:**
```python
assert_equal(bmd.distance(x_test), bmdf.distance(x_test))
```

### Step 2: Assign moving = value

```python
moving = fornix_streamlines()[:20]
```

### Step 3: Assign static = value

```python
static = [s.astype('f8') for s in static]
```

### Step 4: Assign moving = value

```python
moving = [m.astype('f8') for m in moving]
```

### Step 5: Assign bmd = BundleMinDistanceMatrixMetric(...)

```python
bmd = BundleMinDistanceMatrixMetric()
```

### Step 6: Call bmd.setup()

```python
bmd.setup(static, moving)
```

### Step 7: Assign bmdf = BundleMinDistanceMetric(...)

```python
bmdf = BundleMinDistanceMetric()
```

### Step 8: Call bmdf.setup()

```python
bmdf.setup(static, moving)
```

### Step 9: Assign x_test = value

```python
x_test = [0.01, 0, 0, 0, 0, 0]
```

### Step 10: Call print()

```python
print(bmd.distance(x_test))
```

### Step 11: Call print()

```python
print(bmdf.distance(x_test))
```

### Step 12: Call assert_equal()

```python
assert_equal(bmd.distance(x_test), bmdf.distance(x_test))
```


## Complete Example

```python
# Workflow
static = fornix_streamlines()[:20]
moving = fornix_streamlines()[:20]
static = [s.astype('f8') for s in static]
moving = [m.astype('f8') for m in moving]
bmd = BundleMinDistanceMatrixMetric()
bmd.setup(static, moving)
bmdf = BundleMinDistanceMetric()
bmdf.setup(static, moving)
x_test = [0.01, 0, 0, 0, 0, 0]
print(bmd.distance(x_test))
print(bmdf.distance(x_test))
assert_equal(bmd.distance(x_test), bmdf.distance(x_test))
```

## Next Steps


---

*Source: test_streamlinear.py:186 | Complexity: Advanced | Last updated: 2026-05-18*