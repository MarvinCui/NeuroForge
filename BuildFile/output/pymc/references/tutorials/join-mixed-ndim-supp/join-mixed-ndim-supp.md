# How To: Join Mixed Ndim Supp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test join mixed ndim supp

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.tensor.random.type`
- `scipy`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign base1_rv = pt.random.normal(...)

```python
base1_rv = pt.random.normal(size=3, name='base1')
```

### Step 2: Assign base2_rv = pt.random.dirichlet(...)

```python
base2_rv = pt.random.dirichlet(np.ones(3), name='base2')
```

### Step 3: Assign y_rv = pt.concatenate(...)

```python
y_rv = pt.concatenate((base1_rv, base2_rv), axis=0)
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Call logp()

```python
logp(y_rv, y_vv)
```


## Complete Example

```python
# Workflow
base1_rv = pt.random.normal(size=3, name='base1')
base2_rv = pt.random.dirichlet(np.ones(3), name='base2')
y_rv = pt.concatenate((base1_rv, base2_rv), axis=0)
y_vv = y_rv.clone()
with pytest.raises(ValueError, match='Joined logps have different number of dimensions'):
    logp(y_rv, y_vv)
```

## Next Steps


---

*Source: test_tensor.py:355 | Complexity: Intermediate | Last updated: 2026-05-18*