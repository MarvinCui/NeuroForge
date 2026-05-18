# How To: Auto Response Ssst

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test auto response ssst

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
assert_array_equal(response_auto[0], response_from_mask[0])
```

### Step 2: Assign unknown = auto_response_ssst(...)

```python
response_auto, ratio_auto = auto_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
```

**Verification:**
```python
assert_equal(response_auto[1], response_from_mask[1])
```

### Step 3: Assign mask = mask_for_response_ssst(...)

```python
mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
```

**Verification:**
```python
assert_array_equal(ratio_auto, ratio_from_mask)
```

### Step 4: Assign unknown = response_from_mask_ssst(...)

```python
response_from_mask, ratio_from_mask = response_from_mask_ssst(gtab, data, mask)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(response_auto[0], response_from_mask[0])
```

### Step 6: Call assert_equal()

```python
assert_equal(response_auto[1], response_from_mask[1])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(ratio_auto, ratio_from_mask)
```


## Complete Example

```python
# Workflow
gtab, data, _, _, _ = get_test_data()
response_auto, ratio_auto = auto_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
mask = mask_for_response_ssst(gtab, data, roi_center=None, roi_radii=(1, 1, 0), fa_thr=0.7)
response_from_mask, ratio_from_mask = response_from_mask_ssst(gtab, data, mask)
assert_array_equal(response_auto[0], response_from_mask[0])
assert_equal(response_auto[1], response_from_mask[1])
assert_array_equal(ratio_auto, ratio_from_mask)
```

## Next Steps


---

*Source: test_csdeconv.py:226 | Complexity: Intermediate | Last updated: 2026-05-18*