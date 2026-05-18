# How To: With Higher S0

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether fitting works for S0 > 1.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.reconst.ivim`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: '\n    Test whether fitting works for S0 > 1.\n    '

```python
'\n    Test whether fitting works for S0 > 1.\n    '
```

**Verification:**
```python
assert_array_equal(est_signal.shape, data_single2.shape)
```

### Step 2: Assign S0_2 = 1000.0

```python
S0_2 = 1000.0
```

**Verification:**
```python
assert_array_almost_equal(est_signal, data_single2)
```

### Step 3: Assign params2 = np.array(...)

```python
params2 = np.array([S0_2, f, D_star, D])
```

**Verification:**
```python
assert_array_almost_equal(ivim_fit.model_params, params2)
```

### Step 4: Assign mevals2 = np.array(...)

```python
mevals2 = np.array(([D_star, D_star, D_star], [D, D, D]))
```

### Step 5: Assign signal2 = multi_tensor(...)

```python
signal2 = multi_tensor(gtab, mevals2, snr=None, S0=S0_2, fractions=[f * 100, 100 * (1 - f)])
```

### Step 6: Assign data_single2 = value

```python
data_single2 = signal2[0]
```

### Step 7: Assign ivim_fit = ivim_model_trr.fit(...)

```python
ivim_fit = ivim_model_trr.fit(data_single2)
```

### Step 8: Assign est_signal = ivim_fit.predict(...)

```python
est_signal = ivim_fit.predict(gtab)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(est_signal.shape, data_single2.shape)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(est_signal, data_single2)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(ivim_fit.model_params, params2)
```


## Complete Example

```python
# Workflow
'\n    Test whether fitting works for S0 > 1.\n    '
S0_2 = 1000.0
params2 = np.array([S0_2, f, D_star, D])
mevals2 = np.array(([D_star, D_star, D_star], [D, D, D]))
signal2 = multi_tensor(gtab, mevals2, snr=None, S0=S0_2, fractions=[f * 100, 100 * (1 - f)])
data_single2 = signal2[0]
ivim_fit = ivim_model_trr.fit(data_single2)
est_signal = ivim_fit.predict(gtab)
assert_array_equal(est_signal.shape, data_single2.shape)
assert_array_almost_equal(est_signal, data_single2)
assert_array_almost_equal(ivim_fit.model_params, params2)
```

## Next Steps


---

*Source: test_ivim.py:310 | Complexity: Advanced | Last updated: 2026-05-18*