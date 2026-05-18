# How To: Forecast Positive Constrain

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test forecast positive constrain

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
assert_almost_equal(fodf[fodf < 0].sum(), 0, 2)
```

### Step 2: Assign sphere = get_sphere(...)

```python
sphere = get_sphere(name='repulsion100')
```

**Verification:**
```python
assert_almost_equal(coeff[0], c0, 5)
```

### Step 3: Call assert_almost_equal()

```python
assert_almost_equal(fodf[fodf < 0].sum(), 0, 2)
```

### Step 4: Assign coeff = value

```python
coeff = f_fit.sh_coeff
```

### Step 5: Assign c0 = np.sqrt(...)

```python
c0 = np.sqrt(1.0 / (4 * np.pi))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(coeff[0], c0, 5)
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 8: Assign fm = ForecastModel(...)

```python
fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='POS', sphere=data.sphere)
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 10: Assign fodf = f_fit.odf(...)

```python
fodf = f_fit.odf(sphere, clip_negative=False)
```


## Complete Example

```python
# Workflow
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fm = ForecastModel(data.gtab, sh_order_max=data.sh_order_max, lambda_lb=data.lambda_lb, dec_alg='POS', sphere=data.sphere)
f_fit = fm.fit(data.S)
sphere = get_sphere(name='repulsion100')
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    fodf = f_fit.odf(sphere, clip_negative=False)
assert_almost_equal(fodf[fodf < 0].sum(), 0, 2)
coeff = f_fit.sh_coeff
c0 = np.sqrt(1.0 / (4 * np.pi))
assert_almost_equal(coeff[0], c0, 5)
```

## Next Steps


---

*Source: test_forecast.py:45 | Complexity: Advanced | Last updated: 2026-05-18*