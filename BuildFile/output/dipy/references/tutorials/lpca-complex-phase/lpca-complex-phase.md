# How To: Lpca Complex Phase

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca complex phase

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

### Step 1: Assign S0 = value

```python
S0 = 100 * np.exp(1j * np.pi / 4)
```

**Verification:**
```python
assert_array_almost_equal(avg_phase, np.pi / 4, decimal=2)
```

### Step 2: Assign S0_w_noise = value

```python
S0_w_noise = S0 + 2 / np.sqrt(2) * (rng.standard_normal((22, 23, 30, 20)) + 1j * rng.standard_normal((22, 23, 30, 20)))
```

### Step 3: Assign S0_denoised = localpca(...)

```python
S0_denoised = localpca(S0_w_noise, sigma=2)
```

### Step 4: Assign avg_phase = np.angle(...)

```python
avg_phase = np.angle(np.mean(S0_denoised))
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(avg_phase, np.pi / 4, decimal=2)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 100 * np.exp(1j * np.pi / 4)
S0_w_noise = S0 + 2 / np.sqrt(2) * (rng.standard_normal((22, 23, 30, 20)) + 1j * rng.standard_normal((22, 23, 30, 20)))
S0_denoised = localpca(S0_w_noise, sigma=2)
avg_phase = np.angle(np.mean(S0_denoised))
assert_array_almost_equal(avg_phase, np.pi / 4, decimal=2)
```

## Next Steps


---

*Source: test_lpca.py:201 | Complexity: Intermediate | Last updated: 2026-05-18*