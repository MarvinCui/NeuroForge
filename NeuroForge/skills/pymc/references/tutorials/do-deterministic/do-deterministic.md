# How To: Do Deterministic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test do deterministic

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytest`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(seed=435)
```

**Verification:**
```python
assert pm.draw(do_m['z'], random_seed=rng) < 100
```

### Step 2: Assign do_m = do(...)

```python
do_m = do(m, {'z': x - 105})
```

**Verification:**
```python
assert pm.draw(do_m['z'], random_seed=rng) < 100
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 0.001)
```

### Step 4: Assign y = pm.Deterministic(...)

```python
y = pm.Deterministic('y', x + 105)
```

### Step 5: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y, 0.001)
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(seed=435)
with pm.Model() as m:
    x = pm.Normal('x', 0, 0.001)
    y = pm.Deterministic('y', x + 105)
    z = pm.Normal('z', y, 0.001)
do_m = do(m, {'z': x - 105})
assert pm.draw(do_m['z'], random_seed=rng) < 100
```

## Next Steps


---

*Source: test_conditioning.py:211 | Complexity: Intermediate | Last updated: 2026-05-18*