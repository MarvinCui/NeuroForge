# How To: Multivox Forecast

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivox forecast

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

### Step 1: Assign gtab = get_3shell_gtab(...)

```python
gtab = get_3shell_gtab()
```

**Verification:**
```python
assert_equal(S_predict.shape, S.shape)
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0017, 0.0003, 0.0003], [0.0017, 0.0003, 0.0003]))
```

**Verification:**
```python
assert_almost_equal(mse1, 0.0, 3)
```

### Step 3: Assign angl1 = value

```python
angl1 = [(0, 0), (60, 0)]
```

**Verification:**
```python
assert_almost_equal(mse2, 0.0, 3)
```

### Step 4: Assign angl2 = value

```python
angl2 = [(90, 0), (45, 90)]
```

**Verification:**
```python
assert_almost_equal(mse3, 0.0, 3)
```

### Step 5: Assign angl3 = value

```python
angl3 = [(0, 0), (90, 0)]
```

### Step 6: Assign S = np.zeros(...)

```python
S = np.zeros((3, 1, 1, len(gtab.bvals)))
```

### Step 7: Assign unknown = multi_tensor(...)

```python
S[0, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl1, fractions=[50, 50], snr=None)
```

### Step 8: Assign unknown = multi_tensor(...)

```python
S[1, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl2, fractions=[50, 50], snr=None)
```

### Step 9: Assign unknown = multi_tensor(...)

```python
S[2, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl3, fractions=[50, 50], snr=None)
```

### Step 10: Assign f_fit = fm.fit(...)

```python
f_fit = fm.fit(S)
```

### Step 11: Call assert_equal()

```python
assert_equal(S_predict.shape, S.shape)
```

### Step 12: Assign mse1 = value

```python
mse1 = np.sum((S_predict[0, 0, 0] - S[0, 0, 0]) ** 2) / len(gtab.bvals)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(mse1, 0.0, 3)
```

### Step 14: Assign mse2 = value

```python
mse2 = np.sum((S_predict[1, 0, 0] - S[1, 0, 0]) ** 2) / len(gtab.bvals)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(mse2, 0.0, 3)
```

### Step 16: Assign mse3 = value

```python
mse3 = np.sum((S_predict[2, 0, 0] - S[2, 0, 0]) ** 2) / len(gtab.bvals)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(mse3, 0.0, 3)
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(gtab, sh_order_max=8, dec_alg='CSD')
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 21: Assign S_predict = f_fit.predict(...)

```python
S_predict = f_fit.predict()
```


## Complete Example

```python
# Workflow
gtab = get_3shell_gtab()
mevals = np.array(([0.0017, 0.0003, 0.0003], [0.0017, 0.0003, 0.0003]))
angl1 = [(0, 0), (60, 0)]
angl2 = [(90, 0), (45, 90)]
angl3 = [(0, 0), (90, 0)]
S = np.zeros((3, 1, 1, len(gtab.bvals)))
S[0, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl1, fractions=[50, 50], snr=None)
S[1, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl2, fractions=[50, 50], snr=None)
S[2, 0, 0], _ = multi_tensor(gtab, mevals, S0=1.0, angles=angl3, fractions=[50, 50], snr=None)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(gtab, sh_order_max=8, dec_alg='CSD')
f_fit = fm.fit(S)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    S_predict = f_fit.predict()
assert_equal(S_predict.shape, S.shape)
mse1 = np.sum((S_predict[0, 0, 0] - S[0, 0, 0]) ** 2) / len(gtab.bvals)
assert_almost_equal(mse1, 0.0, 3)
mse2 = np.sum((S_predict[1, 0, 0] - S[1, 0, 0]) ** 2) / len(gtab.bvals)
assert_almost_equal(mse2, 0.0, 3)
mse3 = np.sum((S_predict[2, 0, 0] - S[2, 0, 0]) ** 2) / len(gtab.bvals)
assert_almost_equal(mse3, 0.0, 3)
```

## Next Steps


---

*Source: test_forecast.py:318 | Complexity: Advanced | Last updated: 2026-05-18*