# How To: Random Clip

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random clip

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

### Step 1: Assign lb_rv = pt.random.normal(...)

```python
lb_rv = pt.random.normal(0, 1, size=2)
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0, 2)
```

**Verification:**
```python
assert res[0] == -np.inf
```

### Step 3: Assign cens_x_rv = pt.clip(...)

```python
cens_x_rv = pt.clip(x_rv, lb_rv, [1, 1])
```

**Verification:**
```python
assert res[1] != -np.inf
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

### Step 7: Assign logp_combined = pt.add(...)

```python
logp_combined = pt.add(*logp.values())
```

### Step 8: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

### Step 9: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([lb_vv, cens_x_vv], logp_combined)
```

### Step 10: Assign res = logp_fn(...)

```python
res = logp_fn([0, -1], [-1, -1])
```

**Verification:**
```python
assert res[0] == -np.inf
```


## Complete Example

```python
# Workflow
lb_rv = pt.random.normal(0, 1, size=2)
x_rv = pt.random.normal(0, 2)
cens_x_rv = pt.clip(x_rv, lb_rv, [1, 1])
lb_vv = lb_rv.clone()
cens_x_vv = cens_x_rv.clone()
logp = conditional_logp({cens_x_rv: cens_x_vv, lb_rv: lb_vv})
logp_combined = pt.add(*logp.values())
assert_no_rvs(logp_combined)
logp_fn = pytensor.function([lb_vv, cens_x_vv], logp_combined)
res = logp_fn([0, -1], [-1, -1])
assert res[0] == -np.inf
assert res[1] != -np.inf
```

## Next Steps


---

*Source: test_censoring.py:128 | Complexity: Advanced | Last updated: 2026-05-18*