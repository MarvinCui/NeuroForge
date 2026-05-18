# How To: Comparison Invalid Broadcast

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test comparison invalid broadcast

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor`
- `pymc`
- `pymc.logprob`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0.5, 1, size=(3,))
```

### Step 2: Assign const = np.array(...)

```python
const = np.array([[0.1], [0.2], [-0.1]])
```

### Step 3: Assign y_rv_invalid = pt.gt(...)

```python
y_rv_invalid = pt.gt(x_rv, const)
```

### Step 4: Assign y_vv_invalid = y_rv_invalid.clone(...)

```python
y_vv_invalid = y_rv_invalid.clone()
```

### Step 5: Call logp()

```python
logp(y_rv_invalid, y_vv_invalid)
```


## Complete Example

```python
# Workflow
x_rv = pt.random.normal(0.5, 1, size=(3,))
const = np.array([[0.1], [0.2], [-0.1]])
y_rv_invalid = pt.gt(x_rv, const)
y_vv_invalid = y_rv_invalid.clone()
with pytest.raises(NotImplementedError, match='Logprob method not implemented for'):
    logp(y_rv_invalid, y_vv_invalid)
```

## Next Steps


---

*Source: test_binary.py:152 | Complexity: Intermediate | Last updated: 2026-05-18*