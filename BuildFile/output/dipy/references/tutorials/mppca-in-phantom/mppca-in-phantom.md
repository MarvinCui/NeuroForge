# How To: Mppca In Phantom

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test mppca in phantom

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `scipy.special`
- `dipy.core.gradients`
- `dipy.denoise.localpca`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign DWIgt = rfiw_phantom(...)

```python
DWIgt = rfiw_phantom(gtab, snr=None, rng=rng)
```

**Verification:**
```python
assert_(rmse_den < rmse_noisy)
```

### Step 2: Assign std_gt = 0.02

```python
std_gt = 0.02
```

### Step 3: Assign noise = value

```python
noise = std_gt * rng.standard_normal(DWIgt.shape)
```

### Step 4: Assign DWInoise = value

```python
DWInoise = DWIgt + noise
```

### Step 5: Assign rmse_den = value

```python
rmse_den = np.sum(np.abs(DWIgt - DWIden)) / np.sum(np.abs(DWIgt))
```

### Step 6: Assign rmse_noisy = value

```python
rmse_noisy = np.sum(np.abs(DWIgt - DWInoise)) / np.sum(np.abs(DWIgt))
```

### Step 7: Call assert_()

```python
assert_(rmse_den < rmse_noisy)
```

### Step 8: Assign patch_radius_arr = create_patch_radius_arr(...)

```python
patch_radius_arr = create_patch_radius_arr(DWInoise, PR)
```

### Step 9: Assign patch_size = compute_patch_size(...)

```python
patch_size = compute_patch_size(patch_radius_arr)
```

### Step 10: Assign num_samples = compute_num_samples(...)

```python
num_samples = compute_num_samples(patch_size)
```

### Step 11: Assign spr = compute_suggested_patch_radius(...)

```python
spr = compute_suggested_patch_radius(DWInoise, patch_size)
```

### Step 12: Assign DWIden = mppca(...)

```python
DWIden = mppca(DWInoise, patch_radius=PR)
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=dimensionality_problem_message(DWInoise, num_samples, spr), category=UserWarning)
```

### Step 14: Assign DWIden = mppca(...)

```python
DWIden = mppca(DWInoise, patch_radius=PR)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
DWIgt = rfiw_phantom(gtab, snr=None, rng=rng)
std_gt = 0.02
noise = std_gt * rng.standard_normal(DWIgt.shape)
DWInoise = DWIgt + noise
for PR in [2, 1]:
    if PR == 1:
        patch_radius_arr = create_patch_radius_arr(DWInoise, PR)
        patch_size = compute_patch_size(patch_radius_arr)
        num_samples = compute_num_samples(patch_size)
        spr = compute_suggested_patch_radius(DWInoise, patch_size)
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', message=dimensionality_problem_message(DWInoise, num_samples, spr), category=UserWarning)
            DWIden = mppca(DWInoise, patch_radius=PR)
    else:
        DWIden = mppca(DWInoise, patch_radius=PR)
    rmse_den = np.sum(np.abs(DWIgt - DWIden)) / np.sum(np.abs(DWIgt))
    rmse_noisy = np.sum(np.abs(DWIgt - DWInoise)) / np.sum(np.abs(DWIgt))
    assert_(rmse_den < rmse_noisy)
```

## Next Steps


---

*Source: test_lpca.py:410 | Complexity: Advanced | Last updated: 2026-05-18*