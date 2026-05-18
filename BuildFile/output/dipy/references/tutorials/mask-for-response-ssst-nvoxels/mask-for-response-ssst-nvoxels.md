# How To: Mask For Response Ssst Nvoxels

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask for response ssst nvoxels

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.gradients`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign unknown = get_test_data(...)

```python
gtab, data, _, _, _ = get_test_data()
```

**Verification:**
```python
assert_equal(nvoxels, 5)
```

### Step 2: Assign mask = mask_for_response_ssst(...)

```python
mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
```

**Verification:**
```python
assert_equal(nvoxels, 0)
```

### Step 3: Assign nvoxels = np.sum(...)

```python
nvoxels = np.sum(mask)
```

### Step 4: Call assert_equal()

```python
assert_equal(nvoxels, 5)
```

### Step 5: Assign nvoxels = np.sum(...)

```python
nvoxels = np.sum(mask)
```

### Step 6: Call assert_equal()

```python
assert_equal(nvoxels, 0)
```

### Step 7: Assign mask = mask_for_response_ssst(...)

```python
mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=1)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(len(w), 1)
```

### Step 9: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, UserWarning))
```

### Step 10: Call npt.assert_()

```python
npt.assert_('No voxel with a FA higher than 1 were found' in str(w[0].message))
```


## Complete Example

```python
# Workflow
gtab, data, _, _, _ = get_test_data()
mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
nvoxels = np.sum(mask)
assert_equal(nvoxels, 5)
with warnings.catch_warnings(record=True) as w:
    mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=1)
    npt.assert_equal(len(w), 1)
    npt.assert_(issubclass(w[0].category, UserWarning))
    npt.assert_('No voxel with a FA higher than 1 were found' in str(w[0].message))
nvoxels = np.sum(mask)
assert_equal(nvoxels, 0)
```

## Next Steps


---

*Source: test_csdeconv.py:195 | Complexity: Advanced | Last updated: 2026-05-18*