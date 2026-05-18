# How To: Step Discrete

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test step discrete

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

### Step 1: Assign unknown = mv_simple_discrete(...)

```python
start, model, (mu, C) = mv_simple_discrete()
```

### Step 2: Assign unc = value

```python
unc = np.diag(C) ** 0.5
```

### Step 3: Assign check = value

```python
check = (('x', np.mean, mu, unc / 10.0), ('x', np.std, unc, unc / 10.0))
```

### Step 4: Assign step = Metropolis(...)

```python
step = Metropolis(S=C, proposal_dist=MultivariateNormalProposal, rng=123456)
```

### Step 5: Assign idata = pm.sample(...)

```python
idata = pm.sample(tune=1000, draws=2000, chains=1, step=step, initvals=start, model=model, random_seed=1)
```

### Step 6: Call self.check_stat()

```python
self.check_stat(check, idata)
```

### Step 7: Call self.check_stat_dtype()

```python
self.check_stat_dtype(idata, step)
```


## Complete Example

```python
# Workflow
start, model, (mu, C) = mv_simple_discrete()
unc = np.diag(C) ** 0.5
check = (('x', np.mean, mu, unc / 10.0), ('x', np.std, unc, unc / 10.0))
with model:
    step = Metropolis(S=C, proposal_dist=MultivariateNormalProposal, rng=123456)
    idata = pm.sample(tune=1000, draws=2000, chains=1, step=step, initvals=start, model=model, random_seed=1)
    self.check_stat(check, idata)
    self.check_stat_dtype(idata, step)
```

## Next Steps


---

*Source: test_metropolis.py:304 | Complexity: Intermediate | Last updated: 2026-05-18*