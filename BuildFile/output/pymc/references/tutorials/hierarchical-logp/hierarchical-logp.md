# How To: Hierarchical Logp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure there are no random variables in a model's log-likelihood graph.

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

### Step 1: "Make sure there are no random variables in a model's log-likelihood graph."

```python
"Make sure there are no random variables in a model's log-likelihood graph."
```

**Verification:**
```python
assert len(ops) > 0
```

### Step 2: Assign logp_ancestors = list(...)

```python
logp_ancestors = list(ancestors([m.logp()]))
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
assert m.rvs_to_values[x] in logp_ancestors
```

### Step 4: Assign x = pm.Uniform(...)

```python
x = pm.Uniform('x', lower=0, upper=1)
```

**Verification:**
```python
assert m.rvs_to_values[y] in logp_ancestors
```

### Step 5: Assign y = pm.Uniform(...)

```python
y = pm.Uniform('y', lower=0, upper=x)
```


## Complete Example

```python
# Workflow
"Make sure there are no random variables in a model's log-likelihood graph."
with pm.Model() as m:
    x = pm.Uniform('x', lower=0, upper=1)
    y = pm.Uniform('y', lower=0, upper=x)
logp_ancestors = list(ancestors([m.logp()]))
ops = {a.owner.op for a in logp_ancestors if a.owner}
assert len(ops) > 0
assert not any((isinstance(o, RandomVariable) for o in ops))
assert m.rvs_to_values[x] in logp_ancestors
assert m.rvs_to_values[y] in logp_ancestors
```

## Next Steps


---

*Source: test_basic.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*