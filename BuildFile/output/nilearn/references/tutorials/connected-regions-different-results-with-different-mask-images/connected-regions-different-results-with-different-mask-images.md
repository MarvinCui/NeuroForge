# How To: Connected Regions Different Results With Different Mask Images

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test connected regions different results with different mask images

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `scipy.ndimage`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.regions`
- `nilearn.regions.region_extractor`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: maps_and_mask
```

## Step-by-Step Guide

### Step 1: Assign unknown = maps_and_mask

```python
maps, mask_img = maps_and_mask
```

**Verification:**
```python
assert extraction_with_mask_img.shape[-1] >= 1
```

### Step 2: Assign mask = get_data(...)

```python
mask = get_data(mask_img)
```

**Verification:**
```python
assert np.all(get_data(extraction_with_mask_img)[mask == 0] == 0.0)
```

### Step 3: Assign unknown = 0

```python
mask[1, 1, 1] = 0
```

**Verification:**
```python
assert not np.all(get_data(extraction_without_mask_img)[mask == 0] == 0.0)
```

### Step 4: Assign unknown = connected_regions(...)

```python
extraction_with_mask_img, _ = connected_regions(maps, mask_img=mask_img)
```

**Verification:**
```python
assert maps.shape[:3] == extraction_not_same_fov_mask.shape[:3]
```

### Step 5: Assign unknown = connected_regions(...)

```python
extraction_without_mask_img, _ = connected_regions(maps)
```

**Verification:**
```python
assert mask_img.shape != extraction_not_same_fov_mask.shape[:3]
```

### Step 6: Assign mask = np.zeros(...)

```python
mask = np.zeros(shape=(10, 11, 12), dtype='uint8')
```

**Verification:**
```python
assert np.sum(get_data(extraction_not_same_fov) == 0) > np.sum(get_data(extraction_not_same_fov_mask) == 0)
```

### Step 7: Assign unknown = 1

```python
mask[1:-1, 1:-1, 1:-1] = 1
```

### Step 8: Assign affine = np.array(...)

```python
affine = np.array([[2.0, 0.0, 0.0, 0.0], [0.0, 2.0, 0.0, 0.0], [0.0, 0.0, 2.0, 0.0], [0.0, 0.0, 0.0, 2.0]])
```

### Step 9: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine=affine)
```

### Step 10: Assign unknown = connected_regions(...)

```python
extraction_not_same_fov_mask, _ = connected_regions(maps, mask_img=mask_img)
```

**Verification:**
```python
assert maps.shape[:3] == extraction_not_same_fov_mask.shape[:3]
```

### Step 11: Assign unknown = connected_regions(...)

```python
extraction_not_same_fov, _ = connected_regions(maps)
```

**Verification:**
```python
assert np.sum(get_data(extraction_not_same_fov) == 0) > np.sum(get_data(extraction_not_same_fov_mask) == 0)
```


## Complete Example

```python
# Setup
# Fixtures: maps_and_mask

# Workflow
maps, mask_img = maps_and_mask
mask = get_data(mask_img)
mask[1, 1, 1] = 0
extraction_with_mask_img, _ = connected_regions(maps, mask_img=mask_img)
assert extraction_with_mask_img.shape[-1] >= 1
extraction_without_mask_img, _ = connected_regions(maps)
assert np.all(get_data(extraction_with_mask_img)[mask == 0] == 0.0)
assert not np.all(get_data(extraction_without_mask_img)[mask == 0] == 0.0)
mask = np.zeros(shape=(10, 11, 12), dtype='uint8')
mask[1:-1, 1:-1, 1:-1] = 1
affine = np.array([[2.0, 0.0, 0.0, 0.0], [0.0, 2.0, 0.0, 0.0], [0.0, 0.0, 2.0, 0.0], [0.0, 0.0, 0.0, 2.0]])
mask_img = Nifti1Image(mask, affine=affine)
extraction_not_same_fov_mask, _ = connected_regions(maps, mask_img=mask_img)
assert maps.shape[:3] == extraction_not_same_fov_mask.shape[:3]
assert mask_img.shape != extraction_not_same_fov_mask.shape[:3]
extraction_not_same_fov, _ = connected_regions(maps)
assert np.sum(get_data(extraction_not_same_fov) == 0) > np.sum(get_data(extraction_not_same_fov_mask) == 0)
```

## Next Steps


---

*Source: test_region_extractor.py:210 | Complexity: Advanced | Last updated: 2026-05-18*