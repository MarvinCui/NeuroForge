# How To: Elemwise Update Different Scales

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test elemwise update different scales

## Prerequisites

**Required Modules:**
- `warnings`
- `arviz`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytest`
- `pytensor.compile.mode`
- `pymc`
- `pymc.step_methods.metropolis`
- `pymc.step_methods.state`
- `pymc.testing`
- `tests`
- `tests.helpers`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign mu = value

```python
mu = [1, 2, 3, 4, 5, 100, 1000, 10000]
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(trace['x'].mean(('draw', 'chain')), mu, rtol=0.1)
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(trace['x'].var(('draw', 'chain')), mu, rtol=0.2)
```

### Step 4: Assign x = pm.Poisson(...)

```python
x = pm.Poisson('x', mu=mu)
```

### Step 5: Assign step = pm.Metropolis(...)

```python
step = pm.Metropolis([x], rng=SEED)
```

### Step 6: Assign trace = value

```python
trace = pm.sample(draws=1000, chains=2, step=step, random_seed=128).posterior
```


## Complete Example

```python
# Workflow
mu = [1, 2, 3, 4, 5, 100, 1000, 10000]
with pm.Model() as m:
    x = pm.Poisson('x', mu=mu)
    step = pm.Metropolis([x], rng=SEED)
    trace = pm.sample(draws=1000, chains=2, step=step, random_seed=128).posterior
np.testing.assert_allclose(trace['x'].mean(('draw', 'chain')), mu, rtol=0.1)
np.testing.assert_allclose(trace['x'].var(('draw', 'chain')), mu, rtol=0.2)
```

## Next Steps


---

*Source: test_metropolis.py:137 | Complexity: Intermediate | Last updated: 2026-05-18*