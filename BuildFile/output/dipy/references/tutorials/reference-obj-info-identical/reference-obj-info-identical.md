# How To: Reference Obj Info Identical

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reference obj info identical

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `urllib.error`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `trx.trx_file_memmap`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], 'same')
```

**Verification:**
```python
assert_allclose(affine_1, affine_2)
```

### Step 2: Assign trx = tmm.load(...)

```python
trx = tmm.load(FILEPATH_DIX['gs_streamlines.trx'])
```

**Verification:**
```python
assert_array_equal(dimensions_1, dimensions_2)
```

### Step 3: Assign img = nib.load(...)

```python
img = nib.load(FILEPATH_DIX['gs_volume.nii'])
```

**Verification:**
```python
assert_allclose(voxel_sizes_1, voxel_sizes_2)
```

### Step 4: Assign tuple_1 = get_reference_info(...)

```python
tuple_1 = get_reference_info(sft)
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_2
```

### Step 5: Assign tuple_2 = get_reference_info(...)

```python
tuple_2 = get_reference_info(trx)
```

**Verification:**
```python
assert_allclose(affine_1, affine_3)
```

### Step 6: Assign tuple_3 = get_reference_info(...)

```python
tuple_3 = get_reference_info(img)
```

**Verification:**
```python
assert_array_equal(dimensions_1, dimensions_3)
```

### Step 7: Assign unknown = tuple_1

```python
affine_1, dimensions_1, voxel_sizes_1, voxel_order_1 = tuple_1
```

**Verification:**
```python
assert_allclose(voxel_sizes_1, voxel_sizes_3)
```

### Step 8: Assign unknown = tuple_2

```python
affine_2, dimensions_2, voxel_sizes_2, voxel_order_2 = tuple_2
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_3
```

### Step 9: Assign unknown = tuple_3

```python
affine_3, dimensions_3, voxel_sizes_3, voxel_order_3 = tuple_3
```

### Step 10: Call assert_allclose()

```python
assert_allclose(affine_1, affine_2)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(dimensions_1, dimensions_2)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(voxel_sizes_1, voxel_sizes_2)
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_2
```

### Step 13: Call assert_allclose()

```python
assert_allclose(affine_1, affine_3)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(dimensions_1, dimensions_3)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(voxel_sizes_1, voxel_sizes_3)
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_3
```


## Complete Example

```python
# Workflow
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], 'same')
trx = tmm.load(FILEPATH_DIX['gs_streamlines.trx'])
img = nib.load(FILEPATH_DIX['gs_volume.nii'])
tuple_1 = get_reference_info(sft)
tuple_2 = get_reference_info(trx)
tuple_3 = get_reference_info(img)
affine_1, dimensions_1, voxel_sizes_1, voxel_order_1 = tuple_1
affine_2, dimensions_2, voxel_sizes_2, voxel_order_2 = tuple_2
affine_3, dimensions_3, voxel_sizes_3, voxel_order_3 = tuple_3
assert_allclose(affine_1, affine_2)
assert_array_equal(dimensions_1, dimensions_2)
assert_allclose(voxel_sizes_1, voxel_sizes_2)
assert voxel_order_1 == voxel_order_2
assert_allclose(affine_1, affine_3)
assert_array_equal(dimensions_1, dimensions_3)
assert_allclose(voxel_sizes_1, voxel_sizes_3)
assert voxel_order_1 == voxel_order_3
```

## Next Steps


---

*Source: test_utils.py:190 | Complexity: Advanced | Last updated: 2026-05-18*