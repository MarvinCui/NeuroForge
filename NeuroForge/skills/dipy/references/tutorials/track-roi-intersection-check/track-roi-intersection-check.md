# How To: Track Roi Intersection Check

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test track roi intersection check

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

### Step 1: Assign roi = np.array(...)

```python
roi = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0]], dtype='f4')
```

**Verification:**
```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

### Step 2: Assign t = np.array(...)

```python
t = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]], dtype='f4')
```

**Verification:**
```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

### Step 3: Call assert_equal()

```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

**Verification:**
```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

### Step 4: Assign t = np.array(...)

```python
t = np.array([[0, 0, 0], [1, 0, 0], [2, 2, 2]], dtype='f4')
```

**Verification:**
```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), False)
```

### Step 5: Call assert_equal()

```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

### Step 6: Assign t = np.array(...)

```python
t = np.array([[1, 1, 0], [1, 0, 0], [1, -1, 0]], dtype='f4')
```

### Step 7: Call assert_equal()

```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
```

### Step 8: Assign t = np.array(...)

```python
t = np.array([[4, 0, 0], [4, 1, 1], [4, 2, 0]], dtype='f4')
```

### Step 9: Call assert_equal()

```python
assert_equal(pf.track_roi_intersection_check(t, roi, 1), False)
```


## Complete Example

```python
# Workflow
roi = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0]], dtype='f4')
t = np.array([[0, 0, 0], [1, 1, 1], [2, 2, 2]], dtype='f4')
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
t = np.array([[0, 0, 0], [1, 0, 0], [2, 2, 2]], dtype='f4')
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
t = np.array([[1, 1, 0], [1, 0, 0], [1, -1, 0]], dtype='f4')
assert_equal(pf.track_roi_intersection_check(t, roi, 1), True)
t = np.array([[4, 0, 0], [4, 1, 1], [4, 2, 0]], dtype='f4')
assert_equal(pf.track_roi_intersection_check(t, roi, 1), False)
```

## Next Steps


---

*Source: test_distances.py:287 | Complexity: Advanced | Last updated: 2026-05-18*