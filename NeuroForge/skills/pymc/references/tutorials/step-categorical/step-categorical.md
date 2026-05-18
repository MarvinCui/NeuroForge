# How To: Step Categorical

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test step categorical

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: proposal
```

## Step-by-Step Guide

### Step 1: Assign unknown = simple_categorical(...)

```python
start, model, (mu, C) = simple_categorical()
```

### Step 2: Assign unc = value

```python
unc = C ** 0.5
```

### Step 3: Assign check = value

```python
check = (('x', np.mean, mu, unc / 10.0), ('x', np.std, unc, unc / 10.0))
```

### Step 4: Assign step = CategoricalGibbsMetropolis(...)

```python
step = CategoricalGibbsMetropolis([model.x], proposal=proposal, rng=SEED)
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
# Setup
# Fixtures: proposal

# Workflow
start, model, (mu, C) = simple_categorical()
unc = C ** 0.5
check = (('x', np.mean, mu, unc / 10.0), ('x', np.std, unc, unc / 10.0))
with model:
    step = CategoricalGibbsMetropolis([model.x], proposal=proposal, rng=SEED)
    idata = pm.sample(tune=1000, draws=2000, chains=1, step=step, initvals=start, model=model, random_seed=1)
    self.check_stat(check, idata)
    self.check_stat_dtype(idata, step)
```

## Next Steps


---

*Source: test_metropolis.py:323 | Complexity: Intermediate | Last updated: 2026-05-18*