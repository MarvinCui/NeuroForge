# How To: Nutpie End To End

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nutpie end to end

## Prerequisites

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `types`
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pymc`
- `pymc.exceptions`
- `pymc.progress_bar`
- `pymc.step_methods.hmc.quadpotential`


## Step-by-Step Guide

### Step 1: Call HalfNormal()

```python
HalfNormal('sigma')
```

**Verification:**
```python
assert {'posterior', 'sample_stats', 'observed_data'} <= set(idata.children)
```

### Step 2: Call Normal()

```python
Normal('mu')
```

**Verification:**
```python
assert set(idata.posterior.data_vars) == {'mu', 'sigma'}
```

### Step 3: Call Normal()

```python
Normal('y', mu=0, sigma=1, observed=[1.0, 2.0, 3.0])
```

**Verification:**
```python
assert idata.posterior.sizes == {'chain': 2, 'draw': 20}
```

### Step 4: Assign idata = sample(...)

```python
idata = sample(nuts_sampler='nutpie', tune=20, draws=20, chains=2, progressbar=False, random_seed=1411)
```


## Complete Example

```python
# Workflow
with Model() as m:
    HalfNormal('sigma')
    Normal('mu')
    Normal('y', mu=0, sigma=1, observed=[1.0, 2.0, 3.0])
    idata = sample(nuts_sampler='nutpie', tune=20, draws=20, chains=2, progressbar=False, random_seed=1411)
assert {'posterior', 'sample_stats', 'observed_data'} <= set(idata.children)
assert set(idata.posterior.data_vars) == {'mu', 'sigma'}
assert idata.posterior.sizes == {'chain': 2, 'draw': 20}
```

## Next Steps


---

*Source: test_mcmc_external.py:256 | Complexity: Intermediate | Last updated: 2026-05-18*