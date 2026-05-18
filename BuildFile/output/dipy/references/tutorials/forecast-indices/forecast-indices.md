# How To: Forecast Indices

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test forecast indices

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.forecast`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign f_fit = fm.fit(...)

```python
f_fit = fm.fit(data.S)
```

**Verification:**
```python
assert_almost_equal(d_par, data.mevals[0, 0], 5)
```

### Step 2: Assign d_par = value

```python
d_par = f_fit.dpar
```

**Verification:**
```python
assert_almost_equal(d_perp, data.mevals[0, 1], 5)
```

### Step 3: Assign d_perp = value

```python
d_perp = f_fit.dperp
```

**Verification:**
```python
assert_almost_equal(f_fit.fractional_anisotropy(), gt_fa, 2)
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(d_par, data.mevals[0, 0], 5)
```

**Verification:**
```python
assert_almost_equal(f_fit.mean_diffusivity(), gt_md, 5)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(d_perp, data.mevals[0, 1], 5)
```

**Verification:**
```python
assert_almost_equal(d_par, 0.003, 5)
```

### Step 6: Assign gt_fa = np.sqrt(...)

```python
gt_fa = np.sqrt(0.5 * (2 * (data.mevals[0, 0] - data.mevals[0, 1]) ** 2) / (data.mevals[0, 0] ** 2 + 2 * data.mevals[0, 1] ** 2))
```

**Verification:**
```python
assert_almost_equal(d_perp, 0.003, 5)
```

### Step 7: Assign gt_md = value

```python
gt_md = (data.mevals[0, 0] + 2 * data.mevals[0, 1]) / 3.0
```

**Verification:**
```python
assert_almost_equal(f_fit.fractional_anisotropy(), 0.0, 5)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(f_fit.fractional_anisotropy(), gt_fa, 2)
```

**Verification:**
```python
assert_almost_equal(f_fit.mean_diffusivity(), 0.003, 10)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(f_fit.mean_diffusivity(), gt_md, 5)
```

### Step 10: Assign mevals = np.array(...)

```python
mevals = np.array(([0.003, 0.003, 0.003], [0.003, 0.003, 0.003]))
```

### Step 11: Assign data.angl = value

```python
data.angl = [(0, 0), (60, 0)]
```

### Step 12: Assign unknown = multi_tensor(...)

```python
S, sticks = multi_tensor(data.gtab, mevals, S0=100.0, angles=data.angl, fractions=[50, 50], snr=None)
```

### Step 13: Assign f_fit = fm.fit(...)

```python
f_fit = fm.fit(S)
```

### Step 14: Assign d_par = value

```python
d_par = f_fit.dpar
```

### Step 15: Assign d_perp = value

```python
d_perp = f_fit.dperp
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(d_par, 0.003, 5)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(d_perp, 0.003, 5)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(f_fit.fractional_anisotropy(), 0.0, 5)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(f_fit.mean_diffusivity(), 0.003, 10)
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 21: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, sh_order_max=2, lambda_lb=data.lambda_lb, dec_alg='WLS')
```

### Step 22: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 23: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='WLS')
```


## Complete Example

```python
# Workflow
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, sh_order_max=2, lambda_lb=data.lambda_lb, dec_alg='WLS')
f_fit = fm.fit(data.S)
d_par = f_fit.dpar
d_perp = f_fit.dperp
assert_almost_equal(d_par, data.mevals[0, 0], 5)
assert_almost_equal(d_perp, data.mevals[0, 1], 5)
gt_fa = np.sqrt(0.5 * (2 * (data.mevals[0, 0] - data.mevals[0, 1]) ** 2) / (data.mevals[0, 0] ** 2 + 2 * data.mevals[0, 1] ** 2))
gt_md = (data.mevals[0, 0] + 2 * data.mevals[0, 1]) / 3.0
assert_almost_equal(f_fit.fractional_anisotropy(), gt_fa, 2)
assert_almost_equal(f_fit.mean_diffusivity(), gt_md, 5)
mevals = np.array(([0.003, 0.003, 0.003], [0.003, 0.003, 0.003]))
data.angl = [(0, 0), (60, 0)]
S, sticks = multi_tensor(data.gtab, mevals, S0=100.0, angles=data.angl, fractions=[50, 50], snr=None)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='WLS')
f_fit = fm.fit(S)
d_par = f_fit.dpar
d_perp = f_fit.dperp
assert_almost_equal(d_par, 0.003, 5)
assert_almost_equal(d_perp, 0.003, 5)
assert_almost_equal(f_fit.fractional_anisotropy(), 0.0, 5)
assert_almost_equal(f_fit.mean_diffusivity(), 0.003, 10)
```

## Next Steps


---

*Source: test_forecast.py:235 | Complexity: Advanced | Last updated: 2026-05-18*