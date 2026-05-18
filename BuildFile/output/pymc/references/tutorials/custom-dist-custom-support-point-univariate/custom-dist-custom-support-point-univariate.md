# How To: Custom Dist Custom Support Point Univariate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test custom dist custom support point univariate

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

### Step 1: Assign mu_val = np.array.astype(...)

```python
mu_val = np.array(np.random.normal(loc=2, scale=1)).astype(pytensor.config.floatX)
```

**Verification:**
```python
assert isinstance(a.owner.op, CustomDistRV)
```

### Step 2: Assign evaled_support_point = support_point.eval(...)

```python
evaled_support_point = support_point(a).eval({mu: mu_val})
```

**Verification:**
```python
assert evaled_support_point.shape == to_tuple(size)
```

### Step 3: Assign mu = Normal(...)

```python
mu = Normal('mu')
```

**Verification:**
```python
assert np.all(evaled_support_point == mu_val)
```

### Step 4: Assign a = CustomDist(...)

```python
a = CustomDist('a', mu, support_point=density_support_point, size=size)
```


## Complete Example

```python
# Setup
# Fixtures: size

# Workflow
def density_support_point(rv, size, mu):
    return (pt.ones(size) * mu).astype(rv.dtype)
mu_val = np.array(np.random.normal(loc=2, scale=1)).astype(pytensor.config.floatX)
with Model():
    mu = Normal('mu')
    a = CustomDist('a', mu, support_point=density_support_point, size=size)
assert isinstance(a.owner.op, CustomDistRV)
evaled_support_point = support_point(a).eval({mu: mu_val})
assert evaled_support_point.shape == to_tuple(size)
assert np.all(evaled_support_point == mu_val)
```

## Next Steps


---

*Source: test_custom.py:205 | Complexity: Intermediate | Last updated: 2026-05-18*