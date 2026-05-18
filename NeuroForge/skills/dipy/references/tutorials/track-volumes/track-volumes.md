# How To: Track Volumes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test track volumes

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.tracking.vox2track`


## Step-by-Step Guide

### Step 1: Assign vol_dims = value

```python
vol_dims = (1, 2, 3)
```

**Verification:**
```python
assert_array_equal(tcs, ex_counts)
```

### Step 2: Assign tracks = value

```python
tracks = ([[0, 0, 0], [0, 1, 1]],)
```

**Verification:**
```python
assert_array_equal(tes, ex_els)
```

### Step 3: Assign tracks = value

```python
tracks = [np.array(t) for t in tracks]
```

**Verification:**
```python
assert_array_equal(tcs, ex_counts)
```

### Step 4: Assign unknown = tracks_to_expected(...)

```python
ex_counts, ex_els = tracks_to_expected(tracks, vol_dims)
```

**Verification:**
```python
assert_array_equal(tcs, ex_counts)
```

### Step 5: Assign unknown = tvo.track_counts(...)

```python
tcs, tes = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1])
```

**Verification:**
```python
assert_array_equal(tes, ex_els)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(tcs, ex_counts)
```

**Verification:**
```python
assert_array_equal(tcs, ex_counts)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(tes, ex_els)
```

**Verification:**
```python
assert_array_equal(tes, ex_els)
```

### Step 8: Assign tcs = tvo.track_counts(...)

```python
tcs = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1], return_elements=False)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(tcs, ex_counts)
```

### Step 10: Assign vol_dims = value

```python
vol_dims = (5, 10, 15)
```

### Step 11: Assign tracks = value

```python
tracks = ([[-1, 0, 1], [0, 0.1, 0], [1, 1, 1], [1, 1, 1], [2, 2, 2]], [[0.7, 0, 0], [1, 1, 1], [1, 2, 2], [1, 11, 0]])
```

### Step 12: Assign tracks = value

```python
tracks = [np.array(t) for t in tracks]
```

### Step 13: Assign unknown = tracks_to_expected(...)

```python
ex_counts, ex_els = tracks_to_expected(tracks, vol_dims)
```

### Step 14: Assign unknown = tvo.track_counts(...)

```python
tcs, tes = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1])
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(tcs, ex_counts)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(tes, ex_els)
```

### Step 17: Assign vox_sizes = value

```python
vox_sizes = [1.4, 2.1, 3.7]
```

### Step 18: Assign float_tracks = value

```python
float_tracks = [t * vox_sizes for t in tracks]
```

### Step 19: Assign unknown = tvo.track_counts(...)

```python
tcs, tes = tvo.track_counts(float_tracks, vol_dims, vox_sizes=vox_sizes)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(tcs, ex_counts)
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(tes, ex_els)
```


## Complete Example

```python
# Workflow
vol_dims = (1, 2, 3)
tracks = ([[0, 0, 0], [0, 1, 1]],)
tracks = [np.array(t) for t in tracks]
ex_counts, ex_els = tracks_to_expected(tracks, vol_dims)
tcs, tes = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1])
assert_array_equal(tcs, ex_counts)
assert_array_equal(tes, ex_els)
tcs = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1], return_elements=False)
assert_array_equal(tcs, ex_counts)
vol_dims = (5, 10, 15)
tracks = ([[-1, 0, 1], [0, 0.1, 0], [1, 1, 1], [1, 1, 1], [2, 2, 2]], [[0.7, 0, 0], [1, 1, 1], [1, 2, 2], [1, 11, 0]])
tracks = [np.array(t) for t in tracks]
ex_counts, ex_els = tracks_to_expected(tracks, vol_dims)
tcs, tes = tvo.track_counts(tracks, vol_dims, vox_sizes=[1, 1, 1])
assert_array_equal(tcs, ex_counts)
assert_array_equal(tes, ex_els)
vox_sizes = [1.4, 2.1, 3.7]
float_tracks = [t * vox_sizes for t in tracks]
tcs, tes = tvo.track_counts(float_tracks, vol_dims, vox_sizes=vox_sizes)
assert_array_equal(tcs, ex_counts)
assert_array_equal(tes, ex_els)
```

## Next Steps


---

*Source: test_track_volumes.py:34 | Complexity: Advanced | Last updated: 2026-05-18*