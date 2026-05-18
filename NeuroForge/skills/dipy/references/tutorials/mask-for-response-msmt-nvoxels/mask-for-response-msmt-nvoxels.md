# How To: Mask For Response Msmt Nvoxels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask for response msmt nvoxels

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.reconst`
- `dipy.reconst.mcsd`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = get_test_data(...)

```python
gtab, data, _, _ = get_test_data(rng)
```

### Step 2: Call npt.assert_equal()

```python
npt.assert_equal(len(w), 1)
```

### Step 3: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, UserWarning))
```

### Step 4: Call npt.assert_()

```python
npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
```

### Step 5: Assign wm_nvoxels = np.sum(...)

```python
wm_nvoxels = np.sum(wm_mask)
```

### Step 6: Assign gm_nvoxels = np.sum(...)

```python
gm_nvoxels = np.sum(gm_mask)
```

### Step 7: Assign csf_nvoxels = np.sum(...)

```python
csf_nvoxels = np.sum(csf_mask)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(wm_nvoxels, 5)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(gm_nvoxels, 2)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(csf_nvoxels, 2)
```

### Step 11: Assign wm_nvoxels = np.sum(...)

```python
wm_nvoxels = np.sum(wm_mask)
```

### Step 12: Assign gm_nvoxels = np.sum(...)

```python
gm_nvoxels = np.sum(gm_mask)
```

### Step 13: Assign csf_nvoxels = np.sum(...)

```python
csf_nvoxels = np.sum(csf_mask)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(wm_nvoxels, 0)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(gm_nvoxels, 0)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(csf_nvoxels, 0)
```

### Step 17: Assign unknown = mask_for_response_msmt(...)

```python
wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=0.7, gm_fa_thr=0.3, csf_fa_thr=0.15, gm_md_thr=0.001, csf_md_thr=0.0032)
```

### Step 18: Assign unknown = mask_for_response_msmt(...)

```python
wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=1, gm_fa_thr=0, csf_fa_thr=0, gm_md_thr=0, csf_md_thr=0)
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(len(w), 6)
```

### Step 20: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, UserWarning))
```

### Step 21: Call npt.assert_()

```python
npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
```

### Step 22: Call npt.assert_()

```python
npt.assert_('No voxel with a FA higher than 1 were found' in str(w[1].message))
```

### Step 23: Call npt.assert_()

```python
npt.assert_('No voxel with a FA lower than 0 were found' in str(w[2].message))
```

### Step 24: Call npt.assert_()

```python
npt.assert_('No voxel with a MD lower than 0 were found' in str(w[3].message))
```

### Step 25: Call npt.assert_()

```python
npt.assert_('No voxel with a FA lower than 0 were found' in str(w[4].message))
```

### Step 26: Call npt.assert_()

```python
npt.assert_('No voxel with a MD lower than 0 were found' in str(w[5].message))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
gtab, data, _, _ = get_test_data(rng)
with warnings.catch_warnings(record=True) as w:
    wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=0.7, gm_fa_thr=0.3, csf_fa_thr=0.15, gm_md_thr=0.001, csf_md_thr=0.0032)
npt.assert_equal(len(w), 1)
npt.assert_(issubclass(w[0].category, UserWarning))
npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
wm_nvoxels = np.sum(wm_mask)
gm_nvoxels = np.sum(gm_mask)
csf_nvoxels = np.sum(csf_mask)
npt.assert_equal(wm_nvoxels, 5)
npt.assert_equal(gm_nvoxels, 2)
npt.assert_equal(csf_nvoxels, 2)
with warnings.catch_warnings(record=True) as w:
    wm_mask, gm_mask, csf_mask = mask_for_response_msmt(gtab, data, roi_center=None, roi_radii=(1, 1, 0), wm_fa_thr=1, gm_fa_thr=0, csf_fa_thr=0, gm_md_thr=0, csf_md_thr=0)
    npt.assert_equal(len(w), 6)
    npt.assert_(issubclass(w[0].category, UserWarning))
    npt.assert_('Some b-values are higher than 1200.' in str(w[0].message))
    npt.assert_('No voxel with a FA higher than 1 were found' in str(w[1].message))
    npt.assert_('No voxel with a FA lower than 0 were found' in str(w[2].message))
    npt.assert_('No voxel with a MD lower than 0 were found' in str(w[3].message))
    npt.assert_('No voxel with a FA lower than 0 were found' in str(w[4].message))
    npt.assert_('No voxel with a MD lower than 0 were found' in str(w[5].message))
wm_nvoxels = np.sum(wm_mask)
gm_nvoxels = np.sum(gm_mask)
csf_nvoxels = np.sum(csf_mask)
npt.assert_equal(wm_nvoxels, 0)
npt.assert_equal(gm_nvoxels, 0)
npt.assert_equal(csf_nvoxels, 0)
```

## Next Steps


---

*Source: test_mcsd.py:336 | Complexity: Advanced | Last updated: 2026-05-18*