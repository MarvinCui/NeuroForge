# How To: Random Seed

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test random seed

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.ndarray`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.sampling.mcmc`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.testing`
- `tests.models`

**Setup Required:**
```python
# Fixtures: chains, seeds, cores, init
```

## Step-by-Step Guide

### Step 1: Assign allequal = np.all(...)

```python
allequal = np.all(tr1['x'] == tr2['x'])
```

**Verification:**
```python
assert not allequal
```

### Step 2: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 10, initval='prior')
```

**Verification:**
```python
assert allequal
```

### Step 3: Assign tr1 = pm.sample(...)

```python
tr1 = pm.sample(chains=chains, random_seed=seeds, cores=cores, init=init, tune=0, draws=10, return_inferencedata=False, compute_convergence_checks=False)
```

### Step 4: Assign tr2 = pm.sample(...)

```python
tr2 = pm.sample(chains=chains, random_seed=seeds, cores=cores, init=init, tune=0, draws=10, return_inferencedata=False, compute_convergence_checks=False)
```


## Complete Example

```python
# Setup
# Fixtures: chains, seeds, cores, init

# Workflow
with pm.Model():
    x = pm.Normal('x', 0, 10, initval='prior')
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        tr1 = pm.sample(chains=chains, random_seed=seeds, cores=cores, init=init, tune=0, draws=10, return_inferencedata=False, compute_convergence_checks=False)
        tr2 = pm.sample(chains=chains, random_seed=seeds, cores=cores, init=init, tune=0, draws=10, return_inferencedata=False, compute_convergence_checks=False)
allequal = np.all(tr1['x'] == tr2['x'])
if seeds is None:
    assert not allequal
else:
    assert allequal
```

## Next Steps


---

*Source: test_mcmc.py:79 | Complexity: Intermediate | Last updated: 2026-05-18*