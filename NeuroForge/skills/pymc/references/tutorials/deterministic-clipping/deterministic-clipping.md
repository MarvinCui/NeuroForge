# How To: Deterministic Clipping

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test deterministic clipping

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

### Step 1: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0, 1)
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign clip = pt.clip(...)

```python
clip = pt.clip(x_rv, 0, 0)
```

**Verification:**
```python
assert np.isclose(logp_fn(-1, 1), st.norm(0, 1).logpdf(-1) + st.norm(0, 1).logpdf(1))
```

### Step 3: Assign y_rv = pt.random.normal(...)

```python
y_rv = pt.random.normal(clip, 1)
```

### Step 4: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 5: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 6: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x_rv: x_vv, y_rv: y_vv})
```

### Step 7: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 8: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

### Step 9: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([x_vv, y_vv], logp_combined)
```

**Verification:**
```python
assert np.isclose(logp_fn(-1, 1), st.norm(0, 1).logpdf(-1) + st.norm(0, 1).logpdf(1))
```


## Complete Example

```python
# Workflow
x_rv = pt.random.normal(0, 1)
clip = pt.clip(x_rv, 0, 0)
y_rv = pt.random.normal(clip, 1)
x_vv = x_rv.clone()
y_vv = y_rv.clone()
logp = conditional_logp({x_rv: x_vv, y_rv: y_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
logp_fn = pytensor.function([x_vv, y_vv], logp_combined)
assert np.isclose(logp_fn(-1, 1), st.norm(0, 1).logpdf(-1) + st.norm(0, 1).logpdf(1))
```

## Next Steps


---

*Source: test_censoring.py:200 | Complexity: Advanced | Last updated: 2026-05-18*