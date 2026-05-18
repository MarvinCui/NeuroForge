# How To: Read Conte69 Ptseries

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read conte69 ptseries

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `nibabel`
- `nibabel.cifti2`
- `nibabel.tests.nibabel_data`


## Step-by-Step Guide

### Step 1: Assign img = nib.load(...)

```python
img = nib.load(os.path.join(test_directory, 'Conte69.MyelinAndCorrThickness.32k_fs_LR.ptseries.nii'))
```

**Verification:**
```python
assert isinstance(axes[0], cifti2_axes.SeriesAxis)
```

### Step 2: Assign arr = img.get_fdata(...)

```python
arr = img.get_fdata()
```

**Verification:**
```python
assert len(axes[0]) == 2
```

### Step 3: Assign axes = value

```python
axes = [img.header.get_axis(dim) for dim in range(2)]
```

**Verification:**
```python
assert axes[0].start == 0
```

### Step 4: Assign unknown = value

```python
voxels, vertices = axes[1]['ER_FRB08']
```

**Verification:**
```python
assert axes[0].step == 1
```

### Step 5: Call check_rewrite()

```python
check_rewrite(arr, axes)
```

**Verification:**
```python
assert axes[0].size == arr.shape[0]
```


## Complete Example

```python
# Workflow
img = nib.load(os.path.join(test_directory, 'Conte69.MyelinAndCorrThickness.32k_fs_LR.ptseries.nii'))
arr = img.get_fdata()
axes = [img.header.get_axis(dim) for dim in range(2)]
assert isinstance(axes[0], cifti2_axes.SeriesAxis)
assert len(axes[0]) == 2
assert axes[0].start == 0
assert axes[0].step == 1
assert axes[0].size == arr.shape[0]
assert (axes[0].time == [0, 1]).all()
assert len(axes[1]) == 54
voxels, vertices = axes[1]['ER_FRB08']
assert voxels.shape == (0, 3)
assert len(vertices) == 2
assert vertices['CIFTI_STRUCTURE_CORTEX_LEFT'].shape == (206 // 2,)
assert vertices['CIFTI_STRUCTURE_CORTEX_RIGHT'].shape == (206 // 2,)
check_rewrite(arr, axes)
```

## Next Steps


---

*Source: test_cifti2io_axes.py:218 | Complexity: Intermediate | Last updated: 2026-05-18*