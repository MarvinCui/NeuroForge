# How To: Msdeconvfit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test MSDeconvFit

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign gtab = get_3shell_gtab(...)

```python
gtab = get_3shell_gtab()
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([wm_response[0, :3], wm_response[0, :3]])
```

### Step 3: Assign angles = value

```python
angles = [(0, 0), (60, 0)]
```

### Step 4: Assign unknown = multi_tensor(...)

```python
S_wm, sticks = multi_tensor(gtab, mevals, S0=wm_response[0, 3], angles=angles, fractions=[30.0, 70.0], snr=None)
```

### Step 5: Assign S_gm = value

```python
S_gm = gm_response[0, 3] * np.exp(-gtab.bvals * gm_response[0, 0])
```

### Step 6: Assign S_csf = value

```python
S_csf = csf_response[0, 3] * np.exp(-gtab.bvals * csf_response[0, 0])
```

### Step 7: Assign sh_order_max = 8

```python
sh_order_max = 8
```

### Step 8: Assign vf = value

```python
vf = [0.325, 0.2, 0.475]
```

### Step 9: Assign signal = sum(...)

```python
signal = sum((i * j for i, j in zip(vf, [S_csf, S_gm, S_wm])))
```

### Step 10: Assign fit = model.fit(...)

```python
fit = model.fit(signal)
```

### Step 11: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(fit.volume_fractions, vf, 1)
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 13: Assign response = multi_shell_fiber_response(...)

```python
response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
```

### Step 14: Assign model = MultiShellDeconvModel(...)

```python
model = MultiShellDeconvModel(gtab, response)
```


## Complete Example

```python
# Workflow
gtab = get_3shell_gtab()
mevals = np.array([wm_response[0, :3], wm_response[0, :3]])
angles = [(0, 0), (60, 0)]
S_wm, sticks = multi_tensor(gtab, mevals, S0=wm_response[0, 3], angles=angles, fractions=[30.0, 70.0], snr=None)
S_gm = gm_response[0, 3] * np.exp(-gtab.bvals * gm_response[0, 0])
S_csf = csf_response[0, 3] * np.exp(-gtab.bvals * csf_response[0, 0])
sh_order_max = 8
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
    model = MultiShellDeconvModel(gtab, response)
vf = [0.325, 0.2, 0.475]
signal = sum((i * j for i, j in zip(vf, [S_csf, S_gm, S_wm])))
fit = model.fit(signal)
npt.assert_array_almost_equal(fit.volume_fractions, vf, 1)
```

## Next Steps


---

*Source: test_mcsd.py:222 | Complexity: Advanced | Last updated: 2026-05-18*