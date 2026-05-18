# How To: Efficient Bmd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test efficient bmd

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

### Step 1: Assign a = np.array(...)

```python
a = np.array([[1, 1, 1], [2, 2, 2], [3, 3, 3]])
```

**Verification:**
```python
assert_equal(np.sum(np.diag(D)), 0)
```

### Step 2: Assign streamlines = value

```python
streamlines = [a, a + 2, a + 4]
```

**Verification:**
```python
assert_array_almost_equal(D, D2)
```

### Step 3: Assign unknown = unlist_streamlines(...)

```python
points, offsets = unlist_streamlines(streamlines)
```

**Verification:**
```python
assert_almost_equal(dist, dist2)
```

### Step 4: Assign points = points.astype(...)

```python
points = points.astype(np.double)
```

### Step 5: Assign points2 = points.copy(...)

```python
points2 = points.copy()
```

### Step 6: Assign D = np.zeros(...)

```python
D = np.zeros((len(offsets), len(offsets)), dtype='f8')
```

### Step 7: Call _bundle_minimum_distance_matrix()

```python
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets), a.shape[0], D)
```

### Step 8: Call assert_equal()

```python
assert_equal(np.sum(np.diag(D)), 0)
```

### Step 9: Call _bundle_minimum_distance_matrix()

```python
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets), a.shape[0], D)
```

### Step 10: Assign streamlines2 = relist_streamlines(...)

```python
streamlines2 = relist_streamlines(points2, offsets)
```

### Step 11: Assign D2 = distance_matrix_mdf(...)

```python
D2 = distance_matrix_mdf(streamlines, streamlines2)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(D, D2)
```

### Step 13: Assign cols = value

```python
cols = D2.shape[1]
```

### Step 14: Assign rows = value

```python
rows = D2.shape[0]
```

### Step 15: Assign dist = value

```python
dist = 0.25 * (np.sum(np.min(D2, axis=0)) / float(cols) + np.sum(np.min(D2, axis=1)) / float(rows)) ** 2
```

### Step 16: Assign dist2 = _bundle_minimum_distance(...)

```python
dist2 = _bundle_minimum_distance(points, points2, len(offsets), len(offsets), a.shape[0])
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(dist, dist2)
```


## Complete Example

```python
# Workflow
a = np.array([[1, 1, 1], [2, 2, 2], [3, 3, 3]])
streamlines = [a, a + 2, a + 4]
points, offsets = unlist_streamlines(streamlines)
points = points.astype(np.double)
points2 = points.copy()
D = np.zeros((len(offsets), len(offsets)), dtype='f8')
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets), a.shape[0], D)
assert_equal(np.sum(np.diag(D)), 0)
points2 += 2
_bundle_minimum_distance_matrix(points, points2, len(offsets), len(offsets), a.shape[0], D)
streamlines2 = relist_streamlines(points2, offsets)
D2 = distance_matrix_mdf(streamlines, streamlines2)
assert_array_almost_equal(D, D2)
cols = D2.shape[1]
rows = D2.shape[0]
dist = 0.25 * (np.sum(np.min(D2, axis=0)) / float(cols) + np.sum(np.min(D2, axis=1)) / float(rows)) ** 2
dist2 = _bundle_minimum_distance(points, points2, len(offsets), len(offsets), a.shape[0])
assert_almost_equal(dist, dist2)
```

## Next Steps


---

*Source: test_streamlinear.py:219 | Complexity: Advanced | Last updated: 2026-05-18*