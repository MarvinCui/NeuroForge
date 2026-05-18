# How To: Checkparameter

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test CheckParameter

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.graph.replace`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign mu = pt.constant(...)

```python
mu = pt.constant(0)
```

### Step 2: Assign sigma = pt.scalar(...)

```python
sigma = pt.scalar('sigma')
```

### Step 3: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(mu, sigma, name='x')
```

### Step 4: Assign x_vv = pt.constant(...)

```python
x_vv = pt.constant(0)
```

### Step 5: Assign x_logp = logp(...)

```python
x_logp = logp(x_rv, x_vv)
```

### Step 6: Assign x_logp_fn = function(...)

```python
x_logp_fn = function([sigma], x_logp)
```

### Step 7: Call x_logp_fn()

```python
x_logp_fn(-1)
```


## Complete Example

```python
# Workflow
mu = pt.constant(0)
sigma = pt.scalar('sigma')
x_rv = pt.random.normal(mu, sigma, name='x')
x_vv = pt.constant(0)
x_logp = logp(x_rv, x_vv)
x_logp_fn = function([sigma], x_logp)
with pytest.raises(ParameterValueError, match='sigma > 0'):
    x_logp_fn(-1)
```

## Next Steps


---

*Source: test_utils.py:271 | Complexity: Intermediate | Last updated: 2026-05-18*