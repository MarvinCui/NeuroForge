# How To: Exp Transform Rv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test exp transform rv

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`


## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0, 1, size=3, name='base_rv')
```

### Step 2: Assign y_rv = pt.exp(...)

```python
y_rv = pt.exp(base_rv)
```

### Step 3: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([y_vv], logp(y_rv, y_vv))
```

### Step 6: Assign logcdf_fn = pytensor.function(...)

```python
logcdf_fn = pytensor.function([y_vv], logcdf(y_rv, y_vv))
```

### Step 7: Assign icdf_fn = pytensor.function(...)

```python
icdf_fn = pytensor.function([y_vv], icdf(y_rv, y_vv))
```

### Step 8: Assign y_val = value

```python
y_val = [-2.0, 0.1, 0.3]
```

### Step 9: Assign q_val = value

```python
q_val = [0.2, 0.5, 0.9]
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(y_val), sp.stats.lognorm(s=1).logpdf(y_val))
```

### Step 11: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(logcdf_fn(y_val), sp.stats.lognorm(s=1).logcdf(y_val))
```

### Step 12: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(icdf_fn(q_val), sp.stats.lognorm(s=1).ppf(q_val))
```


## Complete Example

```python
# Workflow
base_rv = pt.random.normal(0, 1, size=3, name='base_rv')
y_rv = pt.exp(base_rv)
y_rv.name = 'y'
y_vv = y_rv.clone()
logp_fn = pytensor.function([y_vv], logp(y_rv, y_vv))
logcdf_fn = pytensor.function([y_vv], logcdf(y_rv, y_vv))
icdf_fn = pytensor.function([y_vv], icdf(y_rv, y_vv))
y_val = [-2.0, 0.1, 0.3]
q_val = [0.2, 0.5, 0.9]
np.testing.assert_allclose(logp_fn(y_val), sp.stats.lognorm(s=1).logpdf(y_val))
np.testing.assert_almost_equal(logcdf_fn(y_val), sp.stats.lognorm(s=1).logcdf(y_val))
np.testing.assert_almost_equal(icdf_fn(q_val), sp.stats.lognorm(s=1).ppf(q_val))
```

## Next Steps


---

*Source: test_transforms.py:206 | Complexity: Advanced | Last updated: 2026-05-18*