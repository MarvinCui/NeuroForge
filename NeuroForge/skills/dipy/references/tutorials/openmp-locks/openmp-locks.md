# How To: Openmp Locks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test openmp locks

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign static = value

```python
static = []
```

**Verification:**
```python
assert_almost_equal(dist1, dist2, 6)
```

### Step 2: Assign moving = value

```python
moving = []
```

### Step 3: Assign pts = 20

```python
pts = 20
```

### Step 4: Assign moving = value

```python
moving = moving[2:]
```

### Step 5: Assign unknown = unlist_streamlines(...)

```python
points, offsets = unlist_streamlines(static)
```

### Step 6: Assign unknown = unlist_streamlines(...)

```python
points2, offsets2 = unlist_streamlines(moving)
```

### Step 7: Assign D = np.zeros(...)

```python
D = np.zeros((len(offsets), len(offsets2)), dtype='f8')
```

### Step 8: Call _bundle_minimum_distance_matrix()

```python
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets2), pts, D)
```

### Step 9: Assign dist1 = value

```python
dist1 = 0.25 * (np.sum(np.min(D, axis=0)) / float(D.shape[1]) + np.sum(np.min(D, axis=1)) / float(D.shape[0])) ** 2
```

### Step 10: Assign dist2 = _bundle_minimum_distance(...)

```python
dist2 = _bundle_minimum_distance(points, points2, len(offsets), len(offsets2), pts)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(dist1, dist2, 6)
```

### Step 12: Assign s = rng.random(...)

```python
s = rng.random((pts, 3))
```

### Step 13: Call static.append()

```python
static.append(s)
```

### Step 14: Call moving.append()

```python
moving.append(s + 2)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
static = []
moving = []
pts = 20
for _ in range(1000):
    s = rng.random((pts, 3))
    static.append(s)
    moving.append(s + 2)
moving = moving[2:]
points, offsets = unlist_streamlines(static)
points2, offsets2 = unlist_streamlines(moving)
D = np.zeros((len(offsets), len(offsets2)), dtype='f8')
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets2), pts, D)
dist1 = 0.25 * (np.sum(np.min(D, axis=0)) / float(D.shape[1]) + np.sum(np.min(D, axis=1)) / float(D.shape[0])) ** 2
dist2 = _bundle_minimum_distance(points, points2, len(offsets), len(offsets2), pts)
assert_almost_equal(dist1, dist2, 6)
```

## Next Steps


---

*Source: test_streamlinear.py:266 | Complexity: Advanced | Last updated: 2026-05-18*