# How To: Multiple Rvs To Same Value Raises

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multiple rvs to same value raises

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

### Step 1: Assign x_rv1 = pt.random.normal(...)

```python
x_rv1 = pt.random.normal(name='x1')
```

### Step 2: Assign x_rv2 = pt.random.normal(...)

```python
x_rv2 = pt.random.normal(name='x2')
```

### Step 3: Assign x = x_rv1.type(...)

```python
x = x_rv1.type()
```

### Step 4: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 5: Assign msg = 'More than one logprob term was assigned to the value var x'

```python
msg = 'More than one logprob term was assigned to the value var x'
```

### Step 6: Call conditional_logp()

```python
conditional_logp({x_rv1: x, x_rv2: x})
```


## Complete Example

```python
# Workflow
x_rv1 = pt.random.normal(name='x1')
x_rv2 = pt.random.normal(name='x2')
x = x_rv1.type()
x.name = 'x'
msg = 'More than one logprob term was assigned to the value var x'
with pytest.raises(ValueError, match=msg):
    conditional_logp({x_rv1: x, x_rv2: x})
```

## Next Steps


---

*Source: test_basic.py:220 | Complexity: Intermediate | Last updated: 2026-05-18*