# How To: Multivariate Rv Fails

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test multivariate rv fails

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

### Step 1: Assign _alpha = pt.scalar(...)

```python
_alpha = pt.scalar()
```

### Step 2: Assign _k = pt.iscalar(...)

```python
_k = pt.iscalar()
```

### Step 3: Assign x = pm.StickBreakingWeights.dist(...)

```python
x = pm.StickBreakingWeights.dist(_alpha, _k)
```

### Step 4: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 5: Assign x_m = pt_op(...)

```python
x_m = pt_op(x, axis=-1)
```

### Step 6: Assign x_m_value = pt.scalar(...)

```python
x_m_value = pt.scalar('x_value')
```

### Step 7: Call logp()

```python
logp(x_m, x_m_value)
```


## Complete Example

```python
# Setup
# Fixtures: pt_op

# Workflow
_alpha = pt.scalar()
_k = pt.iscalar()
x = pm.StickBreakingWeights.dist(_alpha, _k)
x.name = 'x'
x_m = pt_op(x, axis=-1)
x_m_value = pt.scalar('x_value')
with pytest.raises(RuntimeError, match=re.escape('Logprob method not implemented')):
    logp(x_m, x_m_value)
```

## Next Steps


---

*Source: test_order.py:87 | Complexity: Intermediate | Last updated: 2026-05-18*