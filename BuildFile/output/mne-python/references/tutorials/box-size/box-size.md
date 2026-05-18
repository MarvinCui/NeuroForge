# How To: Box Size

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test calculation of box sizes.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne.channels`
- `mne.channels.layout`
- `mne.defaults`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test calculation of box sizes.'

```python
'Test calculation of box sizes.'
```

**Verification:**
```python
assert_allclose(_box_size([]), (1.0, 1.0))
```

### Step 2: Call assert_allclose()

```python
assert_allclose(_box_size([]), (1.0, 1.0))
```

**Verification:**
```python
assert_allclose(_box_size(point), (1.0, 1.0))
```

### Step 3: Assign point = value

```python
point = [(0, 0)]
```

**Verification:**
```python
assert_allclose(_box_size(points), (0.5, 1.0))
```

### Step 4: Call assert_allclose()

```python
assert_allclose(_box_size(point), (1.0, 1.0))
```

**Verification:**
```python
assert_allclose(_box_size(points), (0.5, 0.5))
```

### Step 5: Assign points = value

```python
points = [(0.25, 0.5), (0.75, 0.5)]
```

**Verification:**
```python
assert_allclose(_box_size(np.c_[x, y]), (0.1, 0.1))
```

### Step 6: Call assert_allclose()

```python
assert_allclose(_box_size(points), (0.5, 1.0))
```

**Verification:**
```python
assert width is not None
```

### Step 7: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

**Verification:**
```python
assert height is not None
```

### Step 8: Call assert_allclose()

```python
assert_allclose(_box_size(points), (0.5, 0.5))
```

**Verification:**
```python
assert_allclose(_box_size(points, width=0.4), (0.4, 0.5))
```

### Step 9: Assign unknown = np.meshgrid(...)

```python
x, y = np.meshgrid(np.linspace(-0.5, 0.5, 11), np.linspace(-0.5, 0.5, 11))
```

**Verification:**
```python
assert_allclose(_box_size(points, width=0.2), (0.2, 1.0))
```

### Step 10: Assign unknown = value

```python
x, y = (x.ravel(), y.ravel())
```

**Verification:**
```python
assert_allclose(_box_size(points, height=0.4), (0.5, 0.4))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(_box_size(np.c_[x, y]), (0.1, 0.1))
```

**Verification:**
```python
assert_allclose(_box_size(points, height=0.1), (1.0, 0.1))
```

### Step 12: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

**Verification:**
```python
assert_array_equal(_box_size(points, width=0.1, height=0.1), (0.1, 0.1))
```

### Step 13: Assign points = rng.rand(...)

```python
points = rng.rand(100, 2)
```

**Verification:**
```python
assert_array_equal(_box_size(points, width=1), (1, 0))
```

### Step 14: Assign unknown = _box_size(...)

```python
width, height = _box_size(points)
```

**Verification:**
```python
assert_allclose(_box_size(points, padding=0.1), (0.9 * 0.5, 0.9 * 0.5))
```

### Step 15: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

### Step 16: Call assert_allclose()

```python
assert_allclose(_box_size(points, width=0.4), (0.4, 0.5))
```

### Step 17: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

### Step 18: Call assert_allclose()

```python
assert_allclose(_box_size(points, width=0.2), (0.2, 1.0))
```

### Step 19: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

### Step 20: Call assert_allclose()

```python
assert_allclose(_box_size(points, height=0.4), (0.5, 0.4))
```

### Step 21: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.45), (0.5, 0.75)]
```

### Step 22: Call assert_allclose()

```python
assert_allclose(_box_size(points, height=0.1), (1.0, 0.1))
```

### Step 23: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.45), (0.5, 0.75)]
```

### Step 24: Call assert_array_equal()

```python
assert_array_equal(_box_size(points, width=0.1, height=0.1), (0.1, 0.1))
```

### Step 25: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

### Step 26: Call assert_array_equal()

```python
assert_array_equal(_box_size(points, width=1), (1, 0))
```

### Step 27: Assign points = value

```python
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
```

### Step 28: Call assert_allclose()

```python
assert_allclose(_box_size(points, padding=0.1), (0.9 * 0.5, 0.9 * 0.5))
```


## Complete Example

```python
# Workflow
'Test calculation of box sizes.'
assert_allclose(_box_size([]), (1.0, 1.0))
point = [(0, 0)]
assert_allclose(_box_size(point), (1.0, 1.0))
points = [(0.25, 0.5), (0.75, 0.5)]
assert_allclose(_box_size(points), (0.5, 1.0))
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_allclose(_box_size(points), (0.5, 0.5))
x, y = np.meshgrid(np.linspace(-0.5, 0.5, 11), np.linspace(-0.5, 0.5, 11))
x, y = (x.ravel(), y.ravel())
assert_allclose(_box_size(np.c_[x, y]), (0.1, 0.1))
rng = np.random.RandomState(42)
points = rng.rand(100, 2)
width, height = _box_size(points)
assert width is not None
assert height is not None
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_allclose(_box_size(points, width=0.4), (0.4, 0.5))
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_allclose(_box_size(points, width=0.2), (0.2, 1.0))
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_allclose(_box_size(points, height=0.4), (0.5, 0.4))
points = [(0.25, 0.25), (0.75, 0.45), (0.5, 0.75)]
assert_allclose(_box_size(points, height=0.1), (1.0, 0.1))
points = [(0.25, 0.25), (0.75, 0.45), (0.5, 0.75)]
assert_array_equal(_box_size(points, width=0.1, height=0.1), (0.1, 0.1))
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_array_equal(_box_size(points, width=1), (1, 0))
points = [(0.25, 0.25), (0.75, 0.25), (0.5, 0.75)]
assert_allclose(_box_size(points, padding=0.1), (0.9 * 0.5, 0.9 * 0.5))
```

## Next Steps


---

*Source: test_layout.py:318 | Complexity: Advanced | Last updated: 2026-05-18*