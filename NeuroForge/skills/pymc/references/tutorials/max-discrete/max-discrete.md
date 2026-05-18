# How To: Max Discrete

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test max discrete

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc`
- `pymc.logprob`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: mu, size, value, axis
```

## Step-by-Step Guide

### Step 1: Assign x = pm.Poisson.dist(...)

```python
x = pm.Poisson.dist(name='x', mu=mu, size=size)
```

### Step 2: Assign x_max = pt.max(...)

```python
x_max = pt.max(x, axis=axis)
```

### Step 3: Assign x_max_value = pt.scalar(...)

```python
x_max_value = pt.scalar('x_max_value', dtype=x.type.dtype)
```

### Step 4: Assign x_max_logprob = logp(...)

```python
x_max_logprob = logp(x_max, x_max_value)
```

### Step 5: Assign test_value = value

```python
test_value = value
```

### Step 6: Assign n = size

```python
n = size
```

### Step 7: Assign exp_rv = value

```python
exp_rv = sp.poisson(mu).cdf(test_value) ** n
```

### Step 8: Assign exp_rv_prev = value

```python
exp_rv_prev = sp.poisson(mu).cdf(test_value - 1) ** n
```

### Step 9: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.log(exp_rv - exp_rv_prev), x_max_logprob.eval({x_max_value: test_value}), rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: mu, size, value, axis

# Workflow
x = pm.Poisson.dist(name='x', mu=mu, size=size)
x_max = pt.max(x, axis=axis)
x_max_value = pt.scalar('x_max_value', dtype=x.type.dtype)
x_max_logprob = logp(x_max, x_max_value)
test_value = value
n = size
exp_rv = sp.poisson(mu).cdf(test_value) ** n
exp_rv_prev = sp.poisson(mu).cdf(test_value - 1) ** n
np.testing.assert_allclose(np.log(exp_rv - exp_rv_prev), x_max_logprob.eval({x_max_value: test_value}), rtol=1e-06)
```

## Next Steps


---

*Source: test_order.py:225 | Complexity: Advanced | Last updated: 2026-05-18*