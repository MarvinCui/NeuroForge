# How To: Scan Carried Deterministic State

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test logp of scans with carried states downstream of measured variables.

A moving average model with 2 lags is used for testing.

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.raise_op`
- `pytensor.scan.utils`
- `scipy`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.scan`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test logp of scans with carried states downstream of measured variables.\n\n    A moving average model with 2 lags is used for testing.\n    '

```python
'Test logp of scans with carried states downstream of measured variables.\n\n    A moving average model with 2 lags is used for testing.\n    '
```

**Verification:**
```python
assert_no_rvs(logp_expr)
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(490)
```

### Step 3: Assign steps = 99

```python
steps = 99
```

### Step 4: Assign rng_pt = pytensor.shared(...)

```python
rng_pt = pytensor.shared(np.random.default_rng())
```

### Step 5: Assign rho = pt.vector(...)

```python
rho = pt.vector('rho', shape=(2,))
```

### Step 6: Assign sigma = pt.scalar(...)

```python
sigma = pt.scalar('sigma')
```

### Step 7: Assign unknown = pytensor.scan(...)

```python
_eps, ma2, _next_rng = pytensor.scan(fn=ma2_step, outputs_info=[{'initial': pt.arange(2, dtype='float64'), 'taps': range(-2, 0)}, None, rng_pt], non_sequences=[rho, sigma], n_steps=steps, strict=True, name='ma2', return_updates=False)
```

### Step 8: Assign ma2_vv = ma2.clone(...)

```python
ma2_vv = ma2.clone()
```

### Step 9: Assign logp_expr = logp(...)

```python
logp_expr = logp(ma2, ma2_vv)
```

### Step 10: Call assert_no_rvs()

```python
assert_no_rvs(logp_expr)
```

### Step 11: Assign ma2_test = rng.normal(...)

```python
ma2_test = rng.normal(size=(steps,))
```

### Step 12: Assign rho_test = np.array(...)

```python
rho_test = np.array([0.3, 0.7])
```

### Step 13: Assign sigma_test = 0.9

```python
sigma_test = 0.9
```

### Step 14: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(logp_expr.eval({ma2_vv: ma2_test, rho: rho_test, sigma: sigma_test}), ref_logp(ma2_test, rho_test, sigma_test))
```

### Step 15: Assign mu = value

```python
mu = eps_tm1 * rho[0] + eps_tm2 * rho[1]
```

### Step 16: Assign unknown = value

```python
next_rng, y = pt.random.normal(mu, sigma, rng=rng).owner.outputs
```

### Step 17: Assign eps = value

```python
eps = y - mu
```

### Step 18: Assign epsilon_tm2 = 0

```python
epsilon_tm2 = 0
```

### Step 19: Assign epsilon_tm1 = 1

```python
epsilon_tm1 = 1
```

### Step 20: Assign step_logps = np.zeros_like(...)

```python
step_logps = np.zeros_like(values)
```

### Step 21: Assign mu = value

```python
mu = epsilon_tm1 * rho[0] + epsilon_tm2 * rho[1]
```

### Step 22: Assign unknown = stats.norm.logpdf(...)

```python
step_logps[t] = stats.norm.logpdf(value, mu, sigma)
```

### Step 23: Assign epsilon_tm2 = epsilon_tm1

```python
epsilon_tm2 = epsilon_tm1
```

### Step 24: Assign epsilon_tm1 = value

```python
epsilon_tm1 = value - mu
```


## Complete Example

```python
# Workflow
'Test logp of scans with carried states downstream of measured variables.\n\n    A moving average model with 2 lags is used for testing.\n    '
rng = np.random.default_rng(490)
steps = 99
rng_pt = pytensor.shared(np.random.default_rng())
rho = pt.vector('rho', shape=(2,))
sigma = pt.scalar('sigma')

def ma2_step(eps_tm2, eps_tm1, rng, rho, sigma):
    mu = eps_tm1 * rho[0] + eps_tm2 * rho[1]
    next_rng, y = pt.random.normal(mu, sigma, rng=rng).owner.outputs
    eps = y - mu
    return (eps, y, next_rng)
_eps, ma2, _next_rng = pytensor.scan(fn=ma2_step, outputs_info=[{'initial': pt.arange(2, dtype='float64'), 'taps': range(-2, 0)}, None, rng_pt], non_sequences=[rho, sigma], n_steps=steps, strict=True, name='ma2', return_updates=False)

def ref_logp(values, rho, sigma):
    epsilon_tm2 = 0
    epsilon_tm1 = 1
    step_logps = np.zeros_like(values)
    for t, value in enumerate(values):
        mu = epsilon_tm1 * rho[0] + epsilon_tm2 * rho[1]
        step_logps[t] = stats.norm.logpdf(value, mu, sigma)
        epsilon_tm2 = epsilon_tm1
        epsilon_tm1 = value - mu
    return step_logps
ma2_vv = ma2.clone()
logp_expr = logp(ma2, ma2_vv)
assert_no_rvs(logp_expr)
ma2_test = rng.normal(size=(steps,))
rho_test = np.array([0.3, 0.7])
sigma_test = 0.9
np.testing.assert_array_almost_equal(logp_expr.eval({ma2_vv: ma2_test, rho: rho_test, sigma: sigma_test}), ref_logp(ma2_test, rho_test, sigma_test))
```

## Next Steps


---

*Source: test_scan.py:461 | Complexity: Advanced | Last updated: 2026-05-18*