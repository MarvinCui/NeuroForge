# How To: Broadcasted Clip Constant

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test broadcasted clip constant

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

### Step 1: Assign lb_rv = pt.random.uniform(...)

```python
lb_rv = pt.random.uniform(0, 1)
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0, 2)
```

### Step 3: Assign cens_x_rv = pt.clip(...)

```python
cens_x_rv = pt.clip(x_rv, lb_rv, [1, 1])
```

### Step 4: Assign lb_vv = lb_rv.clone(...)

```python
lb_vv = lb_rv.clone()
```

### Step 5: Assign cens_x_vv = cens_x_rv.clone(...)

```python
cens_x_vv = cens_x_rv.clone()
```

### Step 6: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({cens_x_rv: cens_x_vv, lb_rv: lb_vv})
```

### Step 7: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 8: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```


## Complete Example

```python
# Workflow
lb_rv = pt.random.uniform(0, 1)
x_rv = pt.random.normal(0, 2)
cens_x_rv = pt.clip(x_rv, lb_rv, [1, 1])
lb_vv = lb_rv.clone()
cens_x_vv = cens_x_rv.clone()
logp = conditional_logp({cens_x_rv: cens_x_vv, lb_rv: lb_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
```

## Next Steps


---

*Source: test_censoring.py:146 | Complexity: Advanced | Last updated: 2026-05-18*