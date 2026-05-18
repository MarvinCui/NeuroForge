# How To: Custom Dist Multivariate Logp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test custom dist multivariate logp

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `numpy`
- `pytensor`
- `pytensor`
- `pytensor.graph`
- `scipy`
- `pymc.distributions`
- `pymc.distributions.custom`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling`
- `pymc.step_methods`
- `pymc.testing`
- `numpy`

**Setup Required:**
```python
# Fixtures: size
```

## Step-by-Step Guide

### Step 1: Assign supp_shape = 5

```python
supp_shape = 5
```

**Verification:**
```python
assert isinstance(a.owner.op, CustomDistRV)
```

### Step 2: Assign mu_test_value = npr.normal.astype(...)

```python
mu_test_value = npr.normal(loc=0, scale=1, size=supp_shape).astype(pytensor.config.floatX)
```

**Verification:**
```python
assert log_densityf({'a': a_test_value, 'mu': mu_test_value})[0].shape == to_tuple(size)
```

### Step 3: Assign a_test_value = npr.normal.astype(...)

```python
a_test_value = npr.normal(loc=mu_test_value, scale=1, size=(*to_tuple(size), supp_shape)).astype(pytensor.config.floatX)
```

### Step 4: Assign log_densityf = model.compile_logp(...)

```python
log_densityf = model.compile_logp(vars=[a], sum=False)
```

**Verification:**
```python
assert log_densityf({'a': a_test_value, 'mu': mu_test_value})[0].shape == to_tuple(size)
```

### Step 5: Assign mu = Normal(...)

```python
mu = Normal('mu', size=supp_shape)
```

### Step 6: Assign a = CustomDist(...)

```python
a = CustomDist('a', mu, logp=logp, signature='(n)->(n)', size=size)
```


## Complete Example

```python
# Setup
# Fixtures: size

# Workflow
supp_shape = 5
with Model() as model:

    def logp(value, mu):
        return MvNormal.logp(value, mu, pt.eye(mu.shape[-1]))
    mu = Normal('mu', size=supp_shape)
    a = CustomDist('a', mu, logp=logp, signature='(n)->(n)', size=size)
assert isinstance(a.owner.op, CustomDistRV)
mu_test_value = npr.normal(loc=0, scale=1, size=supp_shape).astype(pytensor.config.floatX)
a_test_value = npr.normal(loc=mu_test_value, scale=1, size=(*to_tuple(size), supp_shape)).astype(pytensor.config.floatX)
log_densityf = model.compile_logp(vars=[a], sum=False)
assert log_densityf({'a': a_test_value, 'mu': mu_test_value})[0].shape == to_tuple(size)
```

## Next Steps


---

*Source: test_custom.py:169 | Complexity: Intermediate | Last updated: 2026-05-18*