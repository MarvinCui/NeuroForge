# How To: Non Iid Fails

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test whether the logprob for ```pt.max``` or ```pt.min``` for non i.i.d is correctly rejected

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: pt_op
```

## Step-by-Step Guide

### Step 1: 'Test whether the logprob for ```pt.max``` or ```pt.min``` for non i.i.d is correctly rejected'

```python
'Test whether the logprob for ```pt.max``` or ```pt.min``` for non i.i.d is correctly rejected'
```

### Step 2: Assign x = pm.Normal.dist(...)

```python
x = pm.Normal.dist([0, 1, 2, 3, 4], 1, shape=(5,))
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_m = pt_op(...)

```python
x_m = pt_op(x, axis=-1)
```

### Step 5: Assign x_m_value = pt.scalar(...)

```python
x_m_value = pt.scalar('x_value')
```

### Step 6: Call logp()

```python
logp(x_m, x_m_value)
```


## Complete Example

```python
# Setup
# Fixtures: pt_op

# Workflow
'Test whether the logprob for ```pt.max``` or ```pt.min``` for non i.i.d is correctly rejected'
x = pm.Normal.dist([0, 1, 2, 3, 4], 1, shape=(5,))
x.name = 'x'
x_m = pt_op(x, axis=-1)
x_m_value = pt.scalar('x_value')
with pytest.raises(RuntimeError, match=re.escape('Logprob method not implemented')):
    logp(x_m, x_m_value)
```

## Next Steps


---

*Source: test_order.py:70 | Complexity: Intermediate | Last updated: 2026-05-18*