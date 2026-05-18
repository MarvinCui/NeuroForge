# How To: One Sided Clip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test one sided clip

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
assert_no_rvs(lb_logp)
```

### Step 2: Assign lb_cens_x_rv = pt.clip(...)

```python
lb_cens_x_rv = pt.clip(x_rv, -1, x_rv)
```

**Verification:**
```python
assert_no_rvs(ub_logp)
```

### Step 3: Assign ub_cens_x_rv = pt.clip(...)

```python
ub_cens_x_rv = pt.clip(x_rv, x_rv, 1)
```

**Verification:**
```python
assert np.all(np.array(logp_fn(-2, 2)) == -np.inf)
```

### Step 4: Assign lb_cens_x_vv = lb_cens_x_rv.clone(...)

```python
lb_cens_x_vv = lb_cens_x_rv.clone()
```

**Verification:**
```python
assert np.all(np.array(logp_fn(2, -2)) != -np.inf)
```

### Step 5: Assign ub_cens_x_vv = ub_cens_x_rv.clone(...)

```python
ub_cens_x_vv = ub_cens_x_rv.clone()
```

### Step 6: Assign lb_logp = pt.sum(...)

```python
lb_logp = pt.sum(logp(lb_cens_x_rv, lb_cens_x_vv))
```

### Step 7: Assign ub_logp = pt.sum(...)

```python
ub_logp = pt.sum(logp(ub_cens_x_rv, ub_cens_x_vv))
```

### Step 8: Call assert_no_rvs()

```python
assert_no_rvs(lb_logp)
```

### Step 9: Call assert_no_rvs()

```python
assert_no_rvs(ub_logp)
```

### Step 10: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([lb_cens_x_vv, ub_cens_x_vv], [lb_logp, ub_logp])
```

### Step 11: Assign ref_scipy = st.norm(...)

```python
ref_scipy = st.norm(0, 1)
```

**Verification:**
```python
assert np.all(np.array(logp_fn(-2, 2)) == -np.inf)
```

### Step 12: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(logp_fn(-1, 1), ref_scipy.logcdf(-1))
```

### Step 13: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(logp_fn(1, -1), ref_scipy.logpdf(-1))
```


## Complete Example

```python
# Workflow
x_rv = pt.random.normal(0, 1)
lb_cens_x_rv = pt.clip(x_rv, -1, x_rv)
ub_cens_x_rv = pt.clip(x_rv, x_rv, 1)
lb_cens_x_vv = lb_cens_x_rv.clone()
ub_cens_x_vv = ub_cens_x_rv.clone()
lb_logp = pt.sum(logp(lb_cens_x_rv, lb_cens_x_vv))
ub_logp = pt.sum(logp(ub_cens_x_rv, ub_cens_x_vv))
assert_no_rvs(lb_logp)
assert_no_rvs(ub_logp)
logp_fn = pytensor.function([lb_cens_x_vv, ub_cens_x_vv], [lb_logp, ub_logp])
ref_scipy = st.norm(0, 1)
assert np.all(np.array(logp_fn(-2, 2)) == -np.inf)
assert np.all(np.array(logp_fn(2, -2)) != -np.inf)
np.testing.assert_almost_equal(logp_fn(-1, 1), ref_scipy.logcdf(-1))
np.testing.assert_almost_equal(logp_fn(1, -1), ref_scipy.logpdf(-1))
```

## Next Steps


---

*Source: test_censoring.py:91 | Complexity: Advanced | Last updated: 2026-05-18*