# How To: Argmax

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether the logprob for ```pt.argmax``` is correctly rejected

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

### Step 1: 'Test whether the logprob for ```pt.argmax``` is correctly rejected'

```python
'Test whether the logprob for ```pt.argmax``` is correctly rejected'
```

### Step 2: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(0, 1, size=(3,))
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_argmax = pt.argmax(...)

```python
x_argmax = pt.argmax(x, axis=-1)
```

### Step 5: Assign x_max_value = pt.scalar(...)

```python
x_max_value = pt.scalar('x_max_value', dtype=x_argmax.type.dtype)
```

### Step 6: Call logp()

```python
logp(x_argmax, x_max_value)
```


## Complete Example

```python
# Workflow
'Test whether the logprob for ```pt.argmax``` is correctly rejected'
x = pt.random.normal(0, 1, size=(3,))
x.name = 'x'
x_argmax = pt.argmax(x, axis=-1)
x_max_value = pt.scalar('x_max_value', dtype=x_argmax.type.dtype)
with pytest.raises(RuntimeError, match=re.escape('Logprob method not implemented for Argmax')):
    logp(x_argmax, x_max_value)
```

## Next Steps


---

*Source: test_order.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*