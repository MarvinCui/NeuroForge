# How To: Threshold Stopping Criterion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests that the threshold stopping criterion returns expected
streamline statuses.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.core.ndindex`
- `dipy.testing.decorators`
- `dipy.tracking.stopping_criterion`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'This tests that the threshold stopping criterion returns expected\n    streamline statuses.\n    '

```python
'This tests that the threshold stopping criterion returns expected\n    streamline statuses.\n    '
```

### Step 2: Assign tissue_map = rng.random(...)

```python
tissue_map = rng.random((4, 4, 4))
```

### Step 3: Assign ttc = ThresholdStoppingCriterion(...)

```python
ttc = ThresholdStoppingCriterion(tissue_map.astype('float32'), 0.5)
```

### Step 4: Assign inds = value

```python
inds = [[0, 1.4, 2.2], [0, 2.3, 2.3], [0, 2.2, 1.3], [0, 0.9, 2.2], [0, 2.8, 1.1], [0, 1.1, 3.3], [0, 2.1, 1.9], [0, 3.1, 3.1], [0, 0.1, 0.1], [0, 0.9, 0.5], [0, 0.9, 0.5], [0, 2.9, 0.1]]
```

### Step 5: Assign outside_pts = value

```python
outside_pts = [[100, 100, 100], [0, -1, 1], [0, 10, 2], [0, 0.5, -0.51], [0, -0.51, 0.1]]
```

### Step 6: Assign pts = np.array(...)

```python
pts = np.array(ind, dtype='float64')
```

### Step 7: Assign state = ttc.check_point(...)

```python
state = ttc.check_point(pts)
```

### Step 8: Assign pts = np.array(...)

```python
pts = np.array(pts, dtype='float64')
```

### Step 9: Assign state = ttc.check_point(...)

```python
state = ttc.check_point(pts)
```

### Step 10: Assign res = scipy.ndimage.map_coordinates(...)

```python
res = scipy.ndimage.map_coordinates(tissue_map, np.reshape(pts, (3, 1)), order=1, mode='nearest')
```

### Step 11: Assign pts = np.array(...)

```python
pts = np.array(pts, dtype='float64')
```

### Step 12: Assign state = ttc.check_point(...)

```python
state = ttc.check_point(pts)
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.OUTSIDEIMAGE))
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'This tests that the threshold stopping criterion returns expected\n    streamline statuses.\n    '
tissue_map = rng.random((4, 4, 4))
ttc = ThresholdStoppingCriterion(tissue_map.astype('float32'), 0.5)
for ind in ndindex(tissue_map.shape):
    pts = np.array(ind, dtype='float64')
    state = ttc.check_point(pts)
    if tissue_map[ind] > 0.5:
        npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
    else:
        npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
inds = [[0, 1.4, 2.2], [0, 2.3, 2.3], [0, 2.2, 1.3], [0, 0.9, 2.2], [0, 2.8, 1.1], [0, 1.1, 3.3], [0, 2.1, 1.9], [0, 3.1, 3.1], [0, 0.1, 0.1], [0, 0.9, 0.5], [0, 0.9, 0.5], [0, 2.9, 0.1]]
for pts in inds:
    pts = np.array(pts, dtype='float64')
    state = ttc.check_point(pts)
    res = scipy.ndimage.map_coordinates(tissue_map, np.reshape(pts, (3, 1)), order=1, mode='nearest')
    if res > 0.5:
        npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
    else:
        npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
outside_pts = [[100, 100, 100], [0, -1, 1], [0, 10, 2], [0, 0.5, -0.51], [0, -0.51, 0.1]]
for pts in outside_pts:
    pts = np.array(pts, dtype='float64')
    state = ttc.check_point(pts)
    npt.assert_equal(state, int(StreamlineStatus.OUTSIDEIMAGE))
```

## Next Steps


---

*Source: test_stopping_criterion.py:71 | Complexity: Advanced | Last updated: 2026-05-18*