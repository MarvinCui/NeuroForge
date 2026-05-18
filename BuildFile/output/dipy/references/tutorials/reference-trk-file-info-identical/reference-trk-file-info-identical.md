# How To: Reference Trk File Info Identical

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reference trk file info identical

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

### Step 1: Assign tuple_1 = get_reference_info(...)

```python
tuple_1 = get_reference_info(FILEPATH_DIX['gs_streamlines.trk'])
```

**Verification:**
```python
assert_allclose(affine_1, affine_2)
```

### Step 2: Assign tuple_2 = get_reference_info(...)

```python
tuple_2 = get_reference_info(FILEPATH_DIX['gs_volume.nii'])
```

**Verification:**
```python
assert_array_equal(dimensions_1, dimensions_2)
```

### Step 3: Assign unknown = tuple_1

```python
affine_1, dimensions_1, voxel_sizes_1, voxel_order_1 = tuple_1
```

**Verification:**
```python
assert_allclose(voxel_sizes_1, voxel_sizes_2)
```

### Step 4: Assign unknown = tuple_2

```python
affine_2, dimensions_2, voxel_sizes_2, voxel_order_2 = tuple_2
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_2
```

### Step 5: Call assert_allclose()

```python
assert_allclose(affine_1, affine_2)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(dimensions_1, dimensions_2)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(voxel_sizes_1, voxel_sizes_2)
```

**Verification:**
```python
assert voxel_order_1 == voxel_order_2
```


## Complete Example

```python
# Workflow
tuple_1 = get_reference_info(FILEPATH_DIX['gs_streamlines.trk'])
tuple_2 = get_reference_info(FILEPATH_DIX['gs_volume.nii'])
affine_1, dimensions_1, voxel_sizes_1, voxel_order_1 = tuple_1
affine_2, dimensions_2, voxel_sizes_2, voxel_order_2 = tuple_2
assert_allclose(affine_1, affine_2)
assert_array_equal(dimensions_1, dimensions_2)
assert_allclose(voxel_sizes_1, voxel_sizes_2)
assert voxel_order_1 == voxel_order_2
```

## Next Steps


---

*Source: test_utils.py:166 | Complexity: Intermediate | Last updated: 2026-05-18*