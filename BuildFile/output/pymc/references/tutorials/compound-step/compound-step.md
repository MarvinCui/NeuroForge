# How To: Compound Step

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compound step

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign default_tune_steps = 0

```python
default_tune_steps = 0
```

**Verification:**
```python
assert get_default_tune_steps(step0, None) == 1000
```

### Step 2: Assign default_tune_steps = 50

```python
default_tune_steps = 50
```

**Verification:**
```python
assert get_default_tune_steps(step0, None, default_tune_steps=999) == 999
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

**Verification:**
```python
assert get_default_tune_steps(step0, 999) == 999
```

### Step 4: Assign y = pm.Categorical(...)

```python
y = pm.Categorical('y', p=[0.25, 0.25, 0.5])
```

**Verification:**
```python
assert get_default_tune_steps(step0, 1001) == 1001
```

### Step 5: Assign step0 = pm.CompoundStep(...)

```python
step0 = pm.CompoundStep([pm.NUTS([x]), AlmostPerfectMetropolis([y])])
```

**Verification:**
```python
assert get_default_tune_steps(step1, None) == 50
```

### Step 6: Assign step1 = pm.CompoundStep(...)

```python
step1 = pm.CompoundStep([PerfectMetropolis([x]), AlmostPerfectMetropolis([y])])
```

**Verification:**
```python
assert get_default_tune_steps(step1, None, default_tune_steps=999) == 50
```


## Complete Example

```python
# Workflow
class PerfectMetropolis(pm.Metropolis):
    default_tune_steps = 0

class AlmostPerfectMetropolis(pm.Metropolis):
    default_tune_steps = 50
with pm.Model():
    x = pm.Normal('x')
    y = pm.Categorical('y', p=[0.25, 0.25, 0.5])
    step0 = pm.CompoundStep([pm.NUTS([x]), AlmostPerfectMetropolis([y])])
    step1 = pm.CompoundStep([PerfectMetropolis([x]), AlmostPerfectMetropolis([y])])
assert get_default_tune_steps(step0, None) == 1000
assert get_default_tune_steps(step0, None, default_tune_steps=999) == 999
assert get_default_tune_steps(step0, 999) == 999
assert get_default_tune_steps(step0, 1001) == 1001
assert get_default_tune_steps(step1, None) == 50
assert get_default_tune_steps(step1, None, default_tune_steps=999) == 50
assert get_default_tune_steps(step1, 999) == 999
```

## Next Steps


---

*Source: test_mcmc.py:1047 | Complexity: Intermediate | Last updated: 2026-05-18*