# How To: Do Constant

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test do constant

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: mutable
```

## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(seed=122)
```

**Verification:**
```python
assert pm.draw(do_m['y'], random_seed=rng) > 100
```

### Step 2: Assign do_m = do(...)

```python
do_m = do(m, {m['x']: 105})
```

**Verification:**
```python
assert pm.draw(do_m['y'], random_seed=rng) > 100
```

### Step 3: Assign x = pm.Data(...)

```python
x = pm.Data('x', 0)
```

### Step 4: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, 0.001)
```

### Step 5: Assign m = freeze_dims_and_data(...)

```python
m = freeze_dims_and_data(m, data=['x'])
```


## Complete Example

```python
# Setup
# Fixtures: mutable

# Workflow
rng = np.random.default_rng(seed=122)
with pm.Model() as m:
    x = pm.Data('x', 0)
    y = pm.Normal('y', x, 0.001)
if not mutable:
    m = freeze_dims_and_data(m, data=['x'])
do_m = do(m, {m['x']: 105})
assert pm.draw(do_m['y'], random_seed=rng) > 100
```

## Next Steps


---

*Source: test_conditioning.py:198 | Complexity: Intermediate | Last updated: 2026-05-18*