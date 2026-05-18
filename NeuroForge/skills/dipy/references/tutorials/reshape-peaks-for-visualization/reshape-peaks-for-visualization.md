# How To: Reshape Peaks For Visualization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reshape peaks for visualization

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `pickle`
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.direction.pmf`
- `dipy.io.gradients`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.utils`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign data1 = rng.standard_normal.astype(...)

```python
data1 = rng.standard_normal((10, 5, 3)).astype('float32')
```

**Verification:**
```python
assert_array_equal(data1_reshape.shape, (10, 15))
```

### Step 2: Assign data2 = rng.standard_normal.astype(...)

```python
data2 = rng.standard_normal((10, 2, 5, 3)).astype('float32')
```

**Verification:**
```python
assert_array_equal(data2_reshape.shape, (10, 2, 15))
```

### Step 3: Assign data3 = rng.standard_normal.astype(...)

```python
data3 = rng.standard_normal((10, 2, 12, 5, 3)).astype('float32')
```

**Verification:**
```python
assert_array_equal(data3_reshape.shape, (10, 2, 12, 15))
```

### Step 4: Assign data1_reshape = reshape_peaks_for_visualization(...)

```python
data1_reshape = reshape_peaks_for_visualization(data1)
```

**Verification:**
```python
assert_array_equal(data1_reshape.reshape(10, 5, 3), data1)
```

### Step 5: Assign data2_reshape = reshape_peaks_for_visualization(...)

```python
data2_reshape = reshape_peaks_for_visualization(data2)
```

**Verification:**
```python
assert_array_equal(data2_reshape.reshape(10, 2, 5, 3), data2)
```

### Step 6: Assign data3_reshape = reshape_peaks_for_visualization(...)

```python
data3_reshape = reshape_peaks_for_visualization(data3)
```

**Verification:**
```python
assert_array_equal(data3_reshape.reshape(10, 2, 12, 5, 3), data3)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(data1_reshape.shape, (10, 15))
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data2_reshape.shape, (10, 2, 15))
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data3_reshape.shape, (10, 2, 12, 15))
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(data1_reshape.reshape(10, 5, 3), data1)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(data2_reshape.reshape(10, 2, 5, 3), data2)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(data3_reshape.reshape(10, 2, 12, 5, 3), data3)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
data1 = rng.standard_normal((10, 5, 3)).astype('float32')
data2 = rng.standard_normal((10, 2, 5, 3)).astype('float32')
data3 = rng.standard_normal((10, 2, 12, 5, 3)).astype('float32')
data1_reshape = reshape_peaks_for_visualization(data1)
data2_reshape = reshape_peaks_for_visualization(data2)
data3_reshape = reshape_peaks_for_visualization(data3)
assert_array_equal(data1_reshape.shape, (10, 15))
assert_array_equal(data2_reshape.shape, (10, 2, 15))
assert_array_equal(data3_reshape.shape, (10, 2, 12, 15))
assert_array_equal(data1_reshape.reshape(10, 5, 3), data1)
assert_array_equal(data2_reshape.reshape(10, 2, 5, 3), data2)
assert_array_equal(data3_reshape.reshape(10, 2, 12, 5, 3), data3)
```

## Next Steps


---

*Source: test_peaks.py:791 | Complexity: Advanced | Last updated: 2026-05-18*