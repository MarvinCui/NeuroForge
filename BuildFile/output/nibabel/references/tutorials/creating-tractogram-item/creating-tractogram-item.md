# How To: Creating Tractogram Item

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test creating tractogram item

## Prerequisites

**Required Modules:**
- `copy`
- `operator`
- `unittest`
- `warnings`
- `collections`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `tractogram`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

**Verification:**
```python
assert len(t) == len(streamline)
```

### Step 2: Assign streamline = rng.rand(...)

```python
streamline = rng.rand(rng.randint(10, 50), 3)
```

**Verification:**
```python
assert_array_equal(t.streamline, streamline)
```

### Step 3: Assign colors = rng.rand(...)

```python
colors = rng.rand(len(streamline), 3)
```

**Verification:**
```python
assert_array_equal(list(t), streamline)
```

### Step 4: Assign mean_curvature = 1.11

```python
mean_curvature = 1.11
```

**Verification:**
```python
assert_array_equal(t.data_for_streamline['mean_curvature'], mean_curvature)
```

### Step 5: Assign mean_color = np.array(...)

```python
mean_color = np.array([0, 1, 0], dtype='f4')
```

**Verification:**
```python
assert_array_equal(t.data_for_streamline['mean_color'], mean_color)
```

### Step 6: Assign data_for_streamline = value

```python
data_for_streamline = {'mean_curvature': mean_curvature, 'mean_color': mean_color}
```

**Verification:**
```python
assert_array_equal(t.data_for_points['colors'], colors)
```

### Step 7: Assign data_for_points = value

```python
data_for_points = {'colors': colors}
```

### Step 8: Assign t = TractogramItem(...)

```python
t = TractogramItem(streamline, data_for_streamline, data_for_points)
```

**Verification:**
```python
assert len(t) == len(streamline)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(t.streamline, streamline)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(list(t), streamline)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(t.data_for_streamline['mean_curvature'], mean_curvature)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(t.data_for_streamline['mean_color'], mean_color)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(t.data_for_points['colors'], colors)
```


## Complete Example

```python
# Workflow
rng = np.random.RandomState(42)
streamline = rng.rand(rng.randint(10, 50), 3)
colors = rng.rand(len(streamline), 3)
mean_curvature = 1.11
mean_color = np.array([0, 1, 0], dtype='f4')
data_for_streamline = {'mean_curvature': mean_curvature, 'mean_color': mean_color}
data_for_points = {'colors': colors}
t = TractogramItem(streamline, data_for_streamline, data_for_points)
assert len(t) == len(streamline)
assert_array_equal(t.streamline, streamline)
assert_array_equal(list(t), streamline)
assert_array_equal(t.data_for_streamline['mean_curvature'], mean_curvature)
assert_array_equal(t.data_for_streamline['mean_color'], mean_color)
assert_array_equal(t.data_for_points['colors'], colors)
```

## Next Steps


---

*Source: test_tractogram.py:470 | Complexity: Advanced | Last updated: 2026-05-18*