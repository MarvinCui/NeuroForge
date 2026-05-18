# How To: Point Track Sq Distance

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test point track sq distance

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.streamline`
- `time`


## Step-by-Step Guide

### Step 1: Assign t = np.array(...)

```python
t = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]], dtype='f4')
```

**Verification:**
```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
```

### Step 2: Assign p = np.array(...)

```python
p = np.array([-1, -1.0, -1], dtype='f4')
```

**Verification:**
```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), True)
```

### Step 3: Call assert_equal()

```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
```

**Verification:**
```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
```

### Step 4: (pf.point_track_sq_distance_check(t, p, 2 ** 2), True)

```python
(pf.point_track_sq_distance_check(t, p, 2 ** 2), True)
```

### Step 5: Assign t = np.array(...)

```python
t = np.array([[0, 0, 0], [1, 0, 0], [2, 2, 0]], dtype='f4')
```

### Step 6: Assign p = np.array(...)

```python
p = np.array([0.5, 0, 0], dtype='f4')
```

### Step 7: Call assert_equal()

```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), True)
```

### Step 8: Assign p = np.array(...)

```python
p = np.array([0.5, 1, 0], dtype='f4')
```

### Step 9: Call assert_equal()

```python
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
```


## Complete Example

```python
# Workflow
t = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]], dtype='f4')
p = np.array([-1, -1.0, -1], dtype='f4')
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
(pf.point_track_sq_distance_check(t, p, 2 ** 2), True)
t = np.array([[0, 0, 0], [1, 0, 0], [2, 2, 0]], dtype='f4')
p = np.array([0.5, 0, 0], dtype='f4')
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), True)
p = np.array([0.5, 1, 0], dtype='f4')
assert_equal(pf.point_track_sq_distance_check(t, p, 0.2 ** 2), False)
```

## Next Steps


---

*Source: test_distances.py:275 | Complexity: Advanced | Last updated: 2026-05-18*