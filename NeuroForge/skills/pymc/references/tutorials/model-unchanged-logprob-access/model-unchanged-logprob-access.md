# How To: Model Unchanged Logprob Access

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model unchanged logprob access

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

### Step 1: Assign original_inputs = set(...)

```python
original_inputs = set(pytensor.graph.graph_inputs([c]))
```

**Verification:**
```python
assert original_inputs == new_inputs
```

### Step 2: Call model.logp()

```python
model.logp()
```

### Step 3: Assign new_inputs = set(...)

```python
new_inputs = set(pytensor.graph.graph_inputs([c]))
```

**Verification:**
```python
assert original_inputs == new_inputs
```

### Step 4: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

### Step 5: Assign c = pm.Uniform(...)

```python
c = pm.Uniform('c', lower=a - 1, upper=1)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    a = pm.Normal('a')
    c = pm.Uniform('c', lower=a - 1, upper=1)
original_inputs = set(pytensor.graph.graph_inputs([c]))
model.logp()
new_inputs = set(pytensor.graph.graph_inputs([c]))
assert original_inputs == new_inputs
```

## Next Steps


---

*Source: test_basic.py:263 | Complexity: Intermediate | Last updated: 2026-05-18*