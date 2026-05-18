# How To: Fail Base And Clip Have Values

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test failure when both base_rv and clipped_rv are given value vars

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.stats`
- `pymc`
- `pymc.logprob`
- `pymc.logprob.transform_value`
- `pymc.logprob.transforms`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test failure when both base_rv and clipped_rv are given value vars'

```python
'Test failure when both base_rv and clipped_rv are given value vars'
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0, 1)
```

### Step 3: Assign cens_x_rv = pt.clip(...)

```python
cens_x_rv = pt.clip(x_rv, x_rv, 1)
```

### Step 4: Assign cens_x_rv.name = 'cens_x'

```python
cens_x_rv.name = 'cens_x'
```

### Step 5: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 6: Assign cens_x_vv = cens_x_rv.clone(...)

```python
cens_x_vv = cens_x_rv.clone()
```

### Step 7: Call conditional_logp()

```python
conditional_logp({cens_x_rv: cens_x_vv, x_rv: x_vv})
```


## Complete Example

```python
# Workflow
'Test failure when both base_rv and clipped_rv are given value vars'
x_rv = pt.random.normal(0, 1)
cens_x_rv = pt.clip(x_rv, x_rv, 1)
cens_x_rv.name = 'cens_x'
x_vv = x_rv.clone()
cens_x_vv = cens_x_rv.clone()
with pytest.raises(RuntimeError, match='could not be derived: {cens_x}'):
    conditional_logp({cens_x_rv: cens_x_vv, x_rv: x_vv})
```

## Next Steps


---

*Source: test_censoring.py:174 | Complexity: Intermediate | Last updated: 2026-05-18*