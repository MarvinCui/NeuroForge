# How To: Forecast Csd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test forecast csd

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

### Step 1: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='repulsion100')
```

**Verification:**
```python
assert_equal(value, 1)
```

### Step 2: Assign f_fit = fm.fit(...)

```python
f_fit = fm.fit(data.S)
```

### Step 3: Assign f_fit = fm.fit(...)

```python
f_fit = fm.fit(data.S)
```

### Step 4: Assign value = value

```python
value = fodf_wls[fodf_wls < 0].sum() < fodf_csd[fodf_csd < 0].sum()
```

### Step 5: Call assert_equal()

```python
assert_equal(value, 1)
```

### Step 6: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 7: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, dec_alg='CSD', sphere=data.sphere, lambda_csd=data.lambda_csd)
```

### Step 8: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 9: Assign fodf_csd = f_fit.odf(...)

```python
fodf_csd = f_fit.odf(sphere, clip_negative=False)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='WLS')
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 13: Assign fodf_wls = f_fit.odf(...)

```python
fodf_wls = f_fit.odf(sphere, clip_negative=False)
```


## Complete Example

```python
# Workflow
sphere = get_sphere(name='repulsion100')
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, dec_alg='CSD', sphere=data.sphere, lambda_csd=data.lambda_csd)
f_fit = fm.fit(data.S)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fodf_csd = f_fit.odf(sphere, clip_negative=False)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='WLS')
f_fit = fm.fit(data.S)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fodf_wls = f_fit.odf(sphere, clip_negative=False)
value = fodf_wls[fodf_wls < 0].sum() < fodf_csd[fodf_csd < 0].sum()
assert_equal(value, 1)
```

## Next Steps


---

*Source: test_forecast.py:76 | Complexity: Advanced | Last updated: 2026-05-18*