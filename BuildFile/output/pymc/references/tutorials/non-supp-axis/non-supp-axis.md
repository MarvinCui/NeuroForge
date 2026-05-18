# How To: Non Supp Axis

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test whether the logprob for ```pt.max``` for unsupported axis is correctly rejected

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

### Step 1: 'Test whether the logprob for ```pt.max``` for unsupported axis is correctly rejected'

```python
'Test whether the logprob for ```pt.max``` for unsupported axis is correctly rejected'
```

### Step 2: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(0, 1, size=(3, 3))
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_m = pt_op(...)

```python
x_m = pt_op(x, axis=-1)
```

### Step 5: Assign x_m_value = pt.vector(...)

```python
x_m_value = pt.vector('x_value')
```

### Step 6: Assign x_max_logprob = logp(...)

```python
x_max_logprob = logp(x_m, x_m_value)
```


## Complete Example

```python
# Setup
# Fixtures: pt_op

# Workflow
'Test whether the logprob for ```pt.max``` for unsupported axis is correctly rejected'
x = pt.random.normal(0, 1, size=(3, 3))
x.name = 'x'
x_m = pt_op(x, axis=-1)
x_m_value = pt.vector('x_value')
with pytest.raises(RuntimeError, match=re.escape('Logprob method not implemented')):
    x_max_logprob = logp(x_m, x_m_value)
```

## Next Steps


---

*Source: test_order.py:122 | Complexity: Intermediate | Last updated: 2026-05-18*