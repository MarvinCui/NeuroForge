# How To: Forecast Predict

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test forecast predict

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
assert_almost_equal(mse, 0.0, 3)
```

### Step 2: Assign mse = value

```python
mse = np.sum((S - data.S / 100.0) ** 2) / len(S)
```

### Step 3: Call assert_almost_equal()

```python
assert_almost_equal(mse, 0.0, 3)
```

### Step 4: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 5: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, sh_order_max=8, dec_alg='CSD', sphere=data.sphere)
```

### Step 6: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 7: Assign S = f_fit.predict(...)

```python
S = f_fit.predict(S0=1.0)
```


## Complete Example

```python
# Workflow
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, sh_order_max=8, dec_alg='CSD', sphere=data.sphere)
f_fit = fm.fit(data.S)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    S = f_fit.predict(S0=1.0)
mse = np.sum((S - data.S / 100.0) ** 2) / len(S)
assert_almost_equal(mse, 0.0, 3)
```

## Next Steps


---

*Source: test_forecast.py:294 | Complexity: Intermediate | Last updated: 2026-05-18*