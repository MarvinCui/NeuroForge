# How To: Docstring Example

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test docstring example

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `pymc.distributions`
- `pymc.model.core`
- `pymc.sampling.deterministic`
- `pymc.sampling.forward`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign mu_raw = pm.Normal(...)

```python
mu_raw = pm.Normal('mu_raw', 0, 1, dims='group')
```

**Verification:**
```python
assert 'mu' not in trace.posterior
```

### Step 2: Assign mu = pm.Deterministic(...)

```python
mu = pm.Deterministic('mu', mu_raw.cumsum(), dims='group')
```

**Verification:**
```python
assert 'mu' in trace.posterior
```

### Step 3: Assign trace = pm.sample(...)

```python
trace = pm.sample(var_names=['mu_raw'], chains=2, tune=5, draws=5)
```

### Step 4: Assign trace.posterior = pm.compute_deterministics(...)

```python
trace.posterior = pm.compute_deterministics(trace.posterior, merge_dataset=True)
```


## Complete Example

```python
# Workflow
import pymc as pm
with pm.Model(coords={'group': (0, 2, 4)}) as m:
    mu_raw = pm.Normal('mu_raw', 0, 1, dims='group')
    mu = pm.Deterministic('mu', mu_raw.cumsum(), dims='group')
    trace = pm.sample(var_names=['mu_raw'], chains=2, tune=5, draws=5)
assert 'mu' not in trace.posterior
with m:
    trace.posterior = pm.compute_deterministics(trace.posterior, merge_dataset=True)
assert 'mu' in trace.posterior
```

## Next Steps


---

*Source: test_deterministic.py:74 | Complexity: Intermediate | Last updated: 2026-05-18*