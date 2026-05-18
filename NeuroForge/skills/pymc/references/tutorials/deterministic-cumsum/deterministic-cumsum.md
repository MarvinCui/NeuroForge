# How To: Deterministic Cumsum

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that deterministic cumsum is not affected

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc.logprob.basic`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test that deterministic cumsum is not affected'

```python
'Test that deterministic cumsum is not affected'
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(1, 1, size=5)
```

**Verification:**
```python
assert np.isclose(logp_fn(np.ones(5), np.arange(5) + 1).sum(), st.norm(1, 1).logpdf(1) * 10)
```

### Step 3: Assign cumsum_x_rv = pt.cumsum(...)

```python
cumsum_x_rv = pt.cumsum(x_rv)
```

### Step 4: Assign y_rv = pt.random.normal(...)

```python
y_rv = pt.random.normal(cumsum_x_rv, 1)
```

### Step 5: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 6: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 7: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x_rv: x_vv, y_rv: y_vv})
```

### Step 8: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 9: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

### Step 10: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([x_vv, y_vv], logp_combined)
```

**Verification:**
```python
assert np.isclose(logp_fn(np.ones(5), np.arange(5) + 1).sum(), st.norm(1, 1).logpdf(1) * 10)
```


## Complete Example

```python
# Workflow
'Test that deterministic cumsum is not affected'
x_rv = pt.random.normal(1, 1, size=5)
cumsum_x_rv = pt.cumsum(x_rv)
y_rv = pt.random.normal(cumsum_x_rv, 1)
x_vv = x_rv.clone()
y_vv = y_rv.clone()
logp = conditional_logp({x_rv: x_vv, y_rv: y_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
logp_fn = pytensor.function([x_vv, y_vv], logp_combined)
assert np.isclose(logp_fn(np.ones(5), np.arange(5) + 1).sum(), st.norm(1, 1).logpdf(1) * 10)
```

## Next Steps


---

*Source: test_cumsum.py:104 | Complexity: Advanced | Last updated: 2026-05-18*