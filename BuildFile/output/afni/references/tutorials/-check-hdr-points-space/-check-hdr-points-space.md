# How To:  Check Hdr Points Space

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test  check hdr points space

## Prerequisites

**Required Modules:**
- `__future__`
- `functools`
- `numpy`
- `py3k`
- `orientations`
- `volumeutils`
- `checkwarns`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Call assert_equal()

```python
assert_equal(tv._check_hdr_points_space({}, None), None)
```

**Verification:**
```python
assert_equal(tv._check_hdr_points_space({}, None), None)
```

### Step 2: Call assert_equal()

```python
assert_equal(tv._check_hdr_points_space({}, 'voxmm'), None)
```

**Verification:**
```python
assert_equal(tv._check_hdr_points_space({}, 'voxmm'), None)
```

### Step 3: Call assert_raises()

```python
assert_raises(ValueError, tv._check_hdr_points_space, {}, 'crazy')
```

**Verification:**
```python
assert_raises(ValueError, tv._check_hdr_points_space, {}, 'crazy')
```

### Step 4: Assign hdr = tv.empty_header(...)

```python
hdr = tv.empty_header()
```

**Verification:**
```python
assert_array_equal(hdr['voxel_size'], [0, 0, 0])
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(hdr['voxel_size'], [0, 0, 0])
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
```

### Step 6: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
```

### Step 7: Assign unknown = value

```python
hdr['voxel_size'] = [-2, 3, 4]
```

**Verification:**
```python
assert_raises(UserWarning, tv._check_hdr_points_space, hdr, 'voxel')
```

### Step 8: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
```

**Verification:**
```python
assert_equal(tv._check_hdr_points_space(hdr, 'voxel'), None)
```

### Step 9: Assign unknown = value

```python
hdr['voxel_size'] = [2, 3, 0]
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 10: Assign unknown = value

```python
hdr['voxel_size'] = [2, 3, 4]
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 11: Call assert_equal()

```python
assert_equal(tv._check_hdr_points_space(hdr, 'voxel'), None)
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 12: Assign unknown = value

```python
hdr['voxel_size'] = [2, 3, 4]
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 13: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 14: Assign unknown = 'RAS'

```python
hdr['voxel_order'] = 'RAS'
```

**Verification:**
```python
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

### Step 15: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

**Verification:**
```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 16: Assign unknown = np.diag(...)

```python
hdr['vox_to_ras'] = np.diag([2, 3, 4, 0])
```

**Verification:**
```python
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

### Step 17: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 18: Assign unknown = np.diag(...)

```python
hdr['vox_to_ras'] = np.diag([-2, 3, 4, 1])
```

### Step 19: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 20: Assign unknown = np.diag(...)

```python
hdr['vox_to_ras'] = np.diag([3, 3, 4, 1])
```

### Step 21: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 22: Assign good_aff = np.diag(...)

```python
good_aff = np.diag([2, 3, 4, 1])
```

### Step 23: Assign unknown = good_aff

```python
hdr['vox_to_ras'] = good_aff
```

### Step 24: Call assert_equal()

```python
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

### Step 25: Assign unknown = ''

```python
hdr['voxel_order'] = ''
```

### Step 26: Call assert_raises()

```python
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
```

### Step 27: Assign good_lps = np.dot(...)

```python
good_lps = np.dot(np.diag([-1, -1, 1, 1]), good_aff)
```

### Step 28: Assign unknown = good_lps

```python
hdr['vox_to_ras'] = good_lps
```

### Step 29: Call assert_equal()

```python
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

### Step 30: Call assert_raises()

```python
assert_raises(UserWarning, tv._check_hdr_points_space, hdr, 'voxel')
```


## Complete Example

```python
# Workflow
assert_equal(tv._check_hdr_points_space({}, None), None)
assert_equal(tv._check_hdr_points_space({}, 'voxmm'), None)
assert_raises(ValueError, tv._check_hdr_points_space, {}, 'crazy')
hdr = tv.empty_header()
assert_array_equal(hdr['voxel_size'], [0, 0, 0])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [-2, 3, 4]
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [2, 3, 0]
with ErrorWarnings():
    assert_raises(UserWarning, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [2, 3, 4]
assert_equal(tv._check_hdr_points_space(hdr, 'voxel'), None)
hdr['voxel_size'] = [2, 3, 4]
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['voxel_order'] = 'RAS'
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([2, 3, 4, 0])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([-2, 3, 4, 1])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([3, 3, 4, 1])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
good_aff = np.diag([2, 3, 4, 1])
hdr['vox_to_ras'] = good_aff
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
hdr['voxel_order'] = ''
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
good_lps = np.dot(np.diag([-1, -1, 1, 1]), good_aff)
hdr['vox_to_ras'] = good_lps
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

## Next Steps


---

*Source: test_trackvis.py:276 | Complexity: Advanced | Last updated: 2026-05-18*