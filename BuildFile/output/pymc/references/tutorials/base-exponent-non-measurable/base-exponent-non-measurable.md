# How To: Base Exponent Non Measurable

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test base exponent non measurable

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`


## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal([2])
```

### Step 2: Assign x_raw_rv = pt.random.normal(...)

```python
x_raw_rv = pt.random.normal()
```

### Step 3: Assign x_rv = pt.power(...)

```python
x_rv = pt.power(base_rv, x_raw_rv)
```

### Step 4: Assign x_rv.name = 'x'

```python
x_rv.name = 'x'
```

### Step 5: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 6: Call conditional_logp()

```python
conditional_logp({x_rv: x_vv})
```


## Complete Example

```python
# Workflow
base_rv = pt.random.normal([2])
x_raw_rv = pt.random.normal()
x_rv = pt.power(base_rv, x_raw_rv)
x_rv.name = 'x'
x_vv = x_rv.clone()
with pytest.raises(RuntimeError, match='The logprob terms of the following value variables could not be derived: {x}'):
    conditional_logp({x_rv: x_vv})
```

## Next Steps


---

*Source: test_transforms.py:673 | Complexity: Intermediate | Last updated: 2026-05-18*