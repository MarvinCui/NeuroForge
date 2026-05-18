# How To: Approx Ei Traj

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test approx ei traj

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

### Step 1: Assign segs = 100

```python
segs = 100
```

**Verification:**
```python
assert_equal(len(xyza), 27)
```

### Step 2: Assign t = np.linspace(...)

```python
t = np.linspace(0, 1.75 * 2 * np.pi, segs)
```

**Verification:**
```python
assert_array_equal(xyza, np.array([[1.0, 0.0, 0.0], [4.0, 0.0, 0.0]]))
```

### Step 3: Assign x = t

```python
x = t
```

### Step 4: Assign y = value

```python
y = 5 * np.sin(5 * t)
```

### Step 5: Assign z = np.zeros(...)

```python
z = np.zeros(x.shape)
```

### Step 6: Assign xyz = value

```python
xyz = np.vstack((x, y, z)).T
```

### Step 7: Assign xyza = pf.approx_polygon_track(...)

```python
xyza = pf.approx_polygon_track(xyz)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(xyza), 27)
```

### Step 9: Assign track = np.array(...)

```python
track = np.array([[1.0, 0.0, 0.0], [1.0, 0.0, 0.0], [3.0, 0.0, 0.0], [4.0, 0.0, 0.0]])
```

### Step 10: Assign xyza = pf.approx_polygon_track(...)

```python
xyza = pf.approx_polygon_track(track)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(xyza, np.array([[1.0, 0.0, 0.0], [4.0, 0.0, 0.0]]))
```


## Complete Example

```python
# Workflow
segs = 100
t = np.linspace(0, 1.75 * 2 * np.pi, segs)
x = t
y = 5 * np.sin(5 * t)
z = np.zeros(x.shape)
xyz = np.vstack((x, y, z)).T
xyza = pf.approx_polygon_track(xyz)
assert_equal(len(xyza), 27)
track = np.array([[1.0, 0.0, 0.0], [1.0, 0.0, 0.0], [3.0, 0.0, 0.0], [4.0, 0.0, 0.0]])
xyza = pf.approx_polygon_track(track)
assert_array_equal(xyza, np.array([[1.0, 0.0, 0.0], [4.0, 0.0, 0.0]]))
```

## Next Steps


---

*Source: test_distances.py:211 | Complexity: Advanced | Last updated: 2026-05-18*