# How To: Mask Volume

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask volume

## Prerequisites

**Required Modules:**
- `numpy`


## Step-by-Step Guide

### Step 1: Assign mask_data = np.zeros(...)

```python
mask_data = np.zeros((20, 20, 20), dtype='u1')
```

**Verification:**
```python
assert vol_mm3 == 1000.0
```

### Step 2: Assign unknown = 1

```python
mask_data[5:15, 5:15, 5:15] = 1
```

**Verification:**
```python
assert vol_vox == 1000
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(mask_data, np.eye(4))
```

### Step 4: Assign vol_mm3 = imagestats.mask_volume(...)

```python
vol_mm3 = imagestats.mask_volume(img)
```

### Step 5: Assign vol_vox = imagestats.count_nonzero_voxels(...)

```python
vol_vox = imagestats.count_nonzero_voxels(img)
```

**Verification:**
```python
assert vol_mm3 == 1000.0
```


## Complete Example

```python
# Workflow
mask_data = np.zeros((20, 20, 20), dtype='u1')
mask_data[5:15, 5:15, 5:15] = 1
img = Nifti1Image(mask_data, np.eye(4))
vol_mm3 = imagestats.mask_volume(img)
vol_vox = imagestats.count_nonzero_voxels(img)
assert vol_mm3 == 1000.0
assert vol_vox == 1000
```

## Next Steps


---

*Source: test_imagestats.py:16 | Complexity: Intermediate | Last updated: 2026-05-18*