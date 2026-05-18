# How To: Min Discrete

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test min discrete

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
# Fixtures: mu, n, test_value, axis
```

## Step-by-Step Guide

### Step 1: Assign x = pm.Poisson.dist(...)

```python
x = pm.Poisson.dist(name='x', mu=mu, size=(n,))
```

### Step 2: Assign x_min = pt.min(...)

```python
x_min = pt.min(x, axis=axis)
```

### Step 3: Assign x_min_value = pt.scalar(...)

```python
x_min_value = pt.scalar('x_min_value', dtype=x.type.dtype)
```

### Step 4: Assign x_min_logprob = logp(...)

```python
x_min_logprob = logp(x_min, x_min_value)
```

### Step 5: Assign sf_before = value

```python
sf_before = 1 - sp.poisson(mu).cdf(test_value - 1)
```

### Step 6: Assign sf = value

```python
sf = 1 - sp.poisson(mu).cdf(test_value)
```

### Step 7: Assign expected_logp = np.log(...)

```python
expected_logp = np.log(sf_before ** n - sf ** n)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_min_logprob.eval({x_min_value: test_value}), expected_logp, rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: mu, n, test_value, axis

# Workflow
x = pm.Poisson.dist(name='x', mu=mu, size=(n,))
x_min = pt.min(x, axis=axis)
x_min_value = pt.scalar('x_min_value', dtype=x.type.dtype)
x_min_logprob = logp(x_min, x_min_value)
sf_before = 1 - sp.poisson(mu).cdf(test_value - 1)
sf = 1 - sp.poisson(mu).cdf(test_value)
expected_logp = np.log(sf_before ** n - sf ** n)
np.testing.assert_allclose(x_min_logprob.eval({x_min_value: test_value}), expected_logp, rtol=1e-06)
```

## Next Steps


---

*Source: test_order.py:248 | Complexity: Advanced | Last updated: 2026-05-18*