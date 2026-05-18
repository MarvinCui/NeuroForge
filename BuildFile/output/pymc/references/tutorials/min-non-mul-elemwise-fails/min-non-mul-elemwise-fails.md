# How To: Min Non Mul Elemwise Fails

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether the logprob for ```pt.min``` for non-mul elemwise RVs is rejected correctly

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc`
- `pymc.logprob`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test whether the logprob for ```pt.min``` for non-mul elemwise RVs is rejected correctly'

```python
'Test whether the logprob for ```pt.min``` for non-mul elemwise RVs is rejected correctly'
```

### Step 2: Assign x = pt.log(...)

```python
x = pt.log(pt.random.beta(0, 1, size=(3,)))
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_min = pt.min(...)

```python
x_min = pt.min(x, axis=-1)
```

### Step 5: Assign x_min_value = pt.scalar(...)

```python
x_min_value = pt.scalar('x_min_value')
```

### Step 6: Call logp()

```python
logp(x_min, x_min_value)
```


## Complete Example

```python
# Workflow
'Test whether the logprob for ```pt.min``` for non-mul elemwise RVs is rejected correctly'
x = pt.log(pt.random.beta(0, 1, size=(3,)))
x.name = 'x'
x_min = pt.min(x, axis=-1)
x_min_value = pt.scalar('x_min_value')
with pytest.raises(RuntimeError, match=re.escape('Logprob method not implemented')):
    logp(x_min, x_min_value)
```

## Next Steps


---

*Source: test_order.py:211 | Complexity: Intermediate | Last updated: 2026-05-18*