# How To: Useless Clip

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test useless clip

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
x_rv = pt.random.normal(0.5, 1, size=3)
```

**Verification:**
```python
assert_no_rvs(logprob)
```

### Step 2: Assign cens_x_rv = pt.clip(...)

```python
cens_x_rv = pt.clip(x_rv, x_rv, x_rv)
```

### Step 3: Assign cens_x_vv = cens_x_rv.clone(...)

```python
cens_x_vv = cens_x_rv.clone()
```

### Step 4: Assign logprob = logp(...)

```python
logprob = logp(cens_x_rv, cens_x_vv)
```

### Step 5: Call assert_no_rvs()

```python
assert_no_rvs(logprob)
```

### Step 6: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([cens_x_vv], logprob)
```

### Step 7: Assign ref_scipy = st.norm(...)

```python
ref_scipy = st.norm(0.5, 1)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn([-2, 0, 2]), ref_scipy.logpdf([-2, 0, 2]))
```


## Complete Example

```python
# Workflow
x_rv = pt.random.normal(0.5, 1, size=3)
cens_x_rv = pt.clip(x_rv, x_rv, x_rv)
cens_x_vv = cens_x_rv.clone()
logprob = logp(cens_x_rv, cens_x_vv)
assert_no_rvs(logprob)
logp_fn = pytensor.function([cens_x_vv], logprob)
ref_scipy = st.norm(0.5, 1)
np.testing.assert_allclose(logp_fn([-2, 0, 2]), ref_scipy.logpdf([-2, 0, 2]))
```

## Next Steps


---

*Source: test_censoring.py:113 | Complexity: Advanced | Last updated: 2026-05-18*