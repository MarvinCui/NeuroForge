# How To: Hierarchical Obs Logp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hierarchical obs logp

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.graph.basic`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.op`
- `scipy`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign obs = np.array(...)

```python
obs = np.array([0.5, 0.4, 5, 2])
```

**Verification:**
```python
assert len(ops) > 0
```

### Step 2: Assign logp_ancestors = list(...)

```python
logp_ancestors = list(ancestors([model.logp()]))
```

**Verification:**
```python
assert not any((isinstance(o, RandomVariable) for o in ops))
```

### Step 3: Assign ops = value

```python
ops = {a.owner.op for a in logp_ancestors if a.owner}
```

**Verification:**
```python
assert len(ops) > 0
```

### Step 4: Assign x = pm.Uniform(...)

```python
x = pm.Uniform('x', 0, 1, observed=obs)
```

### Step 5: Call pm.Uniform()

```python
pm.Uniform('y', x, 2, observed=obs)
```


## Complete Example

```python
# Workflow
obs = np.array([0.5, 0.4, 5, 2])
with pm.Model() as model:
    x = pm.Uniform('x', 0, 1, observed=obs)
    pm.Uniform('y', x, 2, observed=obs)
logp_ancestors = list(ancestors([model.logp()]))
ops = {a.owner.op for a in logp_ancestors if a.owner}
assert len(ops) > 0
assert not any((isinstance(o, RandomVariable) for o in ops))
```

## Next Steps


---

*Source: test_basic.py:299 | Complexity: Intermediate | Last updated: 2026-05-18*