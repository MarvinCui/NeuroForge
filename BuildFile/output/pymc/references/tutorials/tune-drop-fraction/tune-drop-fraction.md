# How To: Tune Drop Fraction

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test tune drop fraction

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

### Step 1: Assign tune = 300

```python
tune = 300
```

**Verification:**
```python
assert len(idata.warmup_posterior.draw) == tune
```

### Step 2: Assign tune_drop_fraction = 0.85

```python
tune_drop_fraction = 0.85
```

**Verification:**
```python
assert len(idata.posterior.draw) == draws
```

### Step 3: Assign draws = 200

```python
draws = 200
```

**Verification:**
```python
assert len(step._history) == tune - tune * tune_drop_fraction + draws
```

### Step 4: Call pm.Normal()

```python
pm.Normal('n', 0, 2, size=(3,))
```

### Step 5: Assign step = DEMetropolisZ(...)

```python
step = DEMetropolisZ(tune_drop_fraction=tune_drop_fraction, rng=SEED)
```

### Step 6: Assign idata = pm.sample(...)

```python
idata = pm.sample(tune=tune, draws=draws, step=step, cores=1, chains=1, discard_tuned_samples=False)
```

**Verification:**
```python
assert len(idata.warmup_posterior.draw) == tune
```


## Complete Example

```python
# Workflow
tune = 300
tune_drop_fraction = 0.85
draws = 200
with pm.Model() as pmodel:
    pm.Normal('n', 0, 2, size=(3,))
    step = DEMetropolisZ(tune_drop_fraction=tune_drop_fraction, rng=SEED)
    idata = pm.sample(tune=tune, draws=draws, step=step, cores=1, chains=1, discard_tuned_samples=False)
    assert len(idata.warmup_posterior.draw) == tune
    assert len(idata.posterior.draw) == draws
    assert len(step._history) == tune - tune * tune_drop_fraction + draws
```

## Next Steps


---

*Source: test_metropolis.py:256 | Complexity: Intermediate | Last updated: 2026-05-18*