# How To: Lpca Rmse

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca rmse

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

### Step 1: Assign S0_w_noise = value

```python
S0_w_noise = 100 + 2 * rng.standard_normal((22, 23, 30, 20))
```

**Verification:**
```python
assert_(rmse_denoised < rmse_w_noise)
```

### Step 2: Assign rmse_w_noise = np.sqrt(...)

```python
rmse_w_noise = np.sqrt(np.mean((S0_w_noise - 100) ** 2))
```

### Step 3: Assign S0_denoised = localpca(...)

```python
S0_denoised = localpca(S0_w_noise, sigma=np.std(S0_w_noise))
```

### Step 4: Assign rmse_denoised = np.sqrt(...)

```python
rmse_denoised = np.sqrt(np.mean((S0_denoised - 100) ** 2))
```

### Step 5: Call assert_()

```python
assert_(rmse_denoised < rmse_w_noise)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0_w_noise = 100 + 2 * rng.standard_normal((22, 23, 30, 20))
rmse_w_noise = np.sqrt(np.mean((S0_w_noise - 100) ** 2))
S0_denoised = localpca(S0_w_noise, sigma=np.std(S0_w_noise))
rmse_denoised = np.sqrt(np.mean((S0_denoised - 100) ** 2))
assert_(rmse_denoised < rmse_w_noise)
```

## Next Steps


---

*Source: test_lpca.py:172 | Complexity: Intermediate | Last updated: 2026-05-18*