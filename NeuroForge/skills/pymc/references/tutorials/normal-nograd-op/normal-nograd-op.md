# How To: Normal Nograd Op

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test normal distribution without an implemented gradient is assigned slice method

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

### Step 1: 'Test normal distribution without an implemented gradient is assigned slice method'

```python
'Test normal distribution without an implemented gradient is assigned slice method'
```

**Verification:**
```python
assert selected_steps == {Slice: [model.rvs_to_values[x]]}
```

### Step 2: Assign unknown = assign_step_methods(...)

```python
_, selected_steps = assign_step_methods(model, [])
```

**Verification:**
```python
assert selected_steps == {Slice: [model.rvs_to_values[x]]}
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 1)
```

### Step 4: Assign is_64 = value

```python
is_64 = pytensor.config.floatX == 'float64'
```

### Step 5: Assign itypes = value

```python
itypes = [pt.dscalar] if is_64 else [pt.fscalar]
```

### Step 6: Assign otypes = value

```python
otypes = [pt.dscalar] if is_64 else [pt.fscalar]
```

### Step 7: Assign data = np.random.normal(...)

```python
data = np.random.normal(size=(100,))
```

### Step 8: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', mu=kill_grad(x), sigma=1, observed=data.astype(pytensor.config.floatX))
```


## Complete Example

```python
# Workflow
'Test normal distribution without an implemented gradient is assigned slice method'
with pm.Model() as model:
    x = pm.Normal('x', 0, 1)
    is_64 = pytensor.config.floatX == 'float64'
    itypes = [pt.dscalar] if is_64 else [pt.fscalar]
    otypes = [pt.dscalar] if is_64 else [pt.fscalar]

    @as_op(itypes, otypes)
    def kill_grad(x):
        return x
    data = np.random.normal(size=(100,))
    y = pm.Normal('y', mu=kill_grad(x), sigma=1, observed=data.astype(pytensor.config.floatX))
_, selected_steps = assign_step_methods(model, [])
assert selected_steps == {Slice: [model.rvs_to_values[x]]}
```

## Next Steps


---

*Source: test_mcmc.py:825 | Complexity: Advanced | Last updated: 2026-05-18*