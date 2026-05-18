# How To: Hkernel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the hrf computation.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test the hrf computation.'

```python
'Test the hrf computation.'
```

**Verification:**
```python
assert_almost_equal(h[0], spm_hrf(t_r))
```

### Step 2: Assign t_r = 2.0

```python
t_r = 2.0
```

**Verification:**
```python
assert_almost_equal(h[1], spm_time_derivative(t_r))
```

### Step 3: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('spm', t_r)
```

**Verification:**
```python
assert_almost_equal(h[2], spm_dispersion_derivative(t_r))
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(h[0], spm_hrf(t_r))
```

**Verification:**
```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

### Step 5: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('spm + derivative', t_r)
```

**Verification:**
```python
assert_almost_equal(h[1], glover_time_derivative(t_r))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(h[1], spm_time_derivative(t_r))
```

**Verification:**
```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

### Step 7: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('spm + derivative + dispersion', t_r)
```

**Verification:**
```python
assert_almost_equal(h[2], glover_dispersion_derivative(t_r))
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(h[2], spm_dispersion_derivative(t_r))
```

**Verification:**
```python
assert_almost_equal(h[1], glover_time_derivative(t_r))
```

### Step 9: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('glover', t_r)
```

**Verification:**
```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

**Verification:**
```python
assert_almost_equal(dh.sum(), 1.0)
```

### Step 11: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('glover + derivative', t_r)
```

**Verification:**
```python
assert_almost_equal(h[0], np.hstack((1, np.zeros(49))))
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(h[1], glover_time_derivative(t_r))
```

**Verification:**
```python
assert_almost_equal(h[0], np.ones(100))
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

**Verification:**
```python
assert_almost_equal(h[0], np.ones(100))
```

### Step 14: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('glover + derivative + dispersion', t_r)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(h[2], glover_dispersion_derivative(t_r))
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(h[1], glover_time_derivative(t_r))
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(h[0], glover_hrf(t_r))
```

### Step 18: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('fir', t_r, fir_delays=np.arange(4))
```

### Step 19: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel(None, t_r)
```

### Step 20: Call assert_almost_equal()

```python
assert_almost_equal(h[0], np.hstack((1, np.zeros(49))))
```

### Step 21: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel(lambda t_r, ov: np.ones(int(t_r * ov)), t_r)
```

### Step 22: Call assert_almost_equal()

```python
assert_almost_equal(h[0], np.ones(100))
```

### Step 23: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel([lambda t_r, ov: np.ones(int(t_r * ov))], t_r)
```

### Step 24: Call assert_almost_equal()

```python
assert_almost_equal(h[0], np.ones(100))
```

### Step 25: Call assert_almost_equal()

```python
assert_almost_equal(dh.sum(), 1.0)
```


## Complete Example

```python
# Workflow
'Test the hrf computation.'
t_r = 2.0
h = _hrf_kernel('spm', t_r)
assert_almost_equal(h[0], spm_hrf(t_r))
h = _hrf_kernel('spm + derivative', t_r)
assert_almost_equal(h[1], spm_time_derivative(t_r))
h = _hrf_kernel('spm + derivative + dispersion', t_r)
assert_almost_equal(h[2], spm_dispersion_derivative(t_r))
h = _hrf_kernel('glover', t_r)
assert_almost_equal(h[0], glover_hrf(t_r))
h = _hrf_kernel('glover + derivative', t_r)
assert_almost_equal(h[1], glover_time_derivative(t_r))
assert_almost_equal(h[0], glover_hrf(t_r))
h = _hrf_kernel('glover + derivative + dispersion', t_r)
assert_almost_equal(h[2], glover_dispersion_derivative(t_r))
assert_almost_equal(h[1], glover_time_derivative(t_r))
assert_almost_equal(h[0], glover_hrf(t_r))
h = _hrf_kernel('fir', t_r, fir_delays=np.arange(4))
for dh in h:
    assert_almost_equal(dh.sum(), 1.0)
h = _hrf_kernel(None, t_r)
assert_almost_equal(h[0], np.hstack((1, np.zeros(49))))
h = _hrf_kernel(lambda t_r, ov: np.ones(int(t_r * ov)), t_r)
assert_almost_equal(h[0], np.ones(100))
h = _hrf_kernel([lambda t_r, ov: np.ones(int(t_r * ov))], t_r)
assert_almost_equal(h[0], np.ones(100))
```

## Next Steps


---

*Source: test_hemodynamic_models.py:306 | Complexity: Advanced | Last updated: 2026-05-18*