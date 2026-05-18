# How To: Trim Maps All Regions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Use mask intersecting all regions.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.signal_extraction`

**Setup Required:**
```python
# Fixtures: shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'Use mask intersecting all regions.'

```python
'Use mask intersecting all regions.'
```

**Verification:**
```python
assert maps_i.flags['F_CONTIGUOUS']
```

### Step 2: Assign maps_data = np.zeros(...)

```python
maps_data = np.zeros((*shape_3d_default, N_REGIONS), dtype=np.float32)
```

**Verification:**
```python
assert len(maps_i_indices) == maps_i.shape[-1]
```

### Step 3: Assign unknown = value

```python
h0, h1, h2 = (s // 2 for s in shape_3d_default)
```

**Verification:**
```python
assert maps_i.shape == maps_data.shape
```

### Step 4: Assign unknown = 1

```python
maps_data[:h0, :h1, :h2, 0] = 1
```

**Verification:**
```python
assert_almost_equal(maps_i_correct, maps_i)
```

### Step 5: Assign unknown = 1.1

```python
maps_data[:h0, :h1, h2:, 1] = 1.1
```

**Verification:**
```python
assert_equal(mask_data, maps_i_mask)
```

### Step 6: Assign unknown = 1

```python
maps_data[:h0, h1:, :h2, 2] = 1
```

**Verification:**
```python
assert_equal(np.asarray(list(range(8))), maps_i_indices)
```

### Step 7: Assign unknown = 0.5

```python
maps_data[:h0, h1:, h2:, 3] = 0.5
```

### Step 8: Assign unknown = 1

```python
maps_data[h0:, :h1, :h2, 4] = 1
```

### Step 9: Assign unknown = 1.4

```python
maps_data[h0:, :h1, h2:, 5] = 1.4
```

### Step 10: Assign unknown = 1

```python
maps_data[h0:, h1:, :h2, 6] = 1
```

### Step 11: Assign unknown = 1

```python
maps_data[h0:, h1:, h2:, 7] = 1
```

### Step 12: Assign mask_data = np.zeros(...)

```python
mask_data = np.zeros(shape_3d_default, dtype=np.int8)
```

### Step 13: Assign unknown = 1

```python
mask_data[1:-1, 1:-1, 1:-1] = 1
```

### Step 14: Assign unknown = _trim_maps(...)

```python
maps_i, maps_i_mask, maps_i_indices = _trim_maps(maps_data, mask_data)
```

**Verification:**
```python
assert maps_i.flags['F_CONTIGUOUS']
```

### Step 15: Assign maps_i_correct = maps_data.copy(...)

```python
maps_i_correct = maps_data.copy()
```

### Step 16: Assign unknown = 0

```python
maps_i_correct[np.logical_not(mask_data), :] = 0
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(maps_i_correct, maps_i)
```

### Step 18: Call assert_equal()

```python
assert_equal(mask_data, maps_i_mask)
```

### Step 19: Call assert_equal()

```python
assert_equal(np.asarray(list(range(8))), maps_i_indices)
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'Use mask intersecting all regions.'
maps_data = np.zeros((*shape_3d_default, N_REGIONS), dtype=np.float32)
h0, h1, h2 = (s // 2 for s in shape_3d_default)
maps_data[:h0, :h1, :h2, 0] = 1
maps_data[:h0, :h1, h2:, 1] = 1.1
maps_data[:h0, h1:, :h2, 2] = 1
maps_data[:h0, h1:, h2:, 3] = 0.5
maps_data[h0:, :h1, :h2, 4] = 1
maps_data[h0:, :h1, h2:, 5] = 1.4
maps_data[h0:, h1:, :h2, 6] = 1
maps_data[h0:, h1:, h2:, 7] = 1
mask_data = np.zeros(shape_3d_default, dtype=np.int8)
mask_data[1:-1, 1:-1, 1:-1] = 1
maps_i, maps_i_mask, maps_i_indices = _trim_maps(maps_data, mask_data)
assert maps_i.flags['F_CONTIGUOUS']
assert len(maps_i_indices) == maps_i.shape[-1]
assert maps_i.shape == maps_data.shape
maps_i_correct = maps_data.copy()
maps_i_correct[np.logical_not(mask_data), :] = 0
assert_almost_equal(maps_i_correct, maps_i)
assert_equal(mask_data, maps_i_mask)
assert_equal(np.asarray(list(range(8))), maps_i_indices)
```

## Next Steps


---

*Source: test_signal_extraction.py:738 | Complexity: Advanced | Last updated: 2026-05-18*