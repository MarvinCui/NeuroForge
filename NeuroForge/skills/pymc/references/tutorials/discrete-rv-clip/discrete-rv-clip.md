# How To: Discrete Rv Clip

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test discrete rv clip

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

### Step 1: Assign x_rv = pt.random.poisson(...)

```python
x_rv = pt.random.poisson(2)
```

**Verification:**
```python
assert_no_rvs(logprob)
```

### Step 2: Assign cens_x_rv = pt.clip(...)

```python
cens_x_rv = pt.clip(x_rv, 1, 4)
```

**Verification:**
```python
assert logp_fn(0) == -np.inf
```

### Step 3: Assign cens_x_vv = cens_x_rv.clone(...)

```python
cens_x_vv = cens_x_rv.clone()
```

**Verification:**
```python
assert logp_fn(5) == -np.inf
```

### Step 4: Assign logprob = pt.sum(...)

```python
logprob = pt.sum(logp(cens_x_rv, cens_x_vv))
```

**Verification:**
```python
assert np.isclose(logp_fn(1), ref_scipy.logcdf(1))
```

### Step 5: Call assert_no_rvs()

```python
assert_no_rvs(logprob)
```

**Verification:**
```python
assert np.isclose(logp_fn(4), np.logaddexp(ref_scipy.logsf(4), ref_scipy.logpmf(4)))
```

### Step 6: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([cens_x_vv], logprob)
```

**Verification:**
```python
assert np.isclose(logp_fn(2), ref_scipy.logpmf(2))
```

### Step 7: Assign ref_scipy = st.poisson(...)

```python
ref_scipy = st.poisson(2)
```

**Verification:**
```python
assert logp_fn(0) == -np.inf
```


## Complete Example

```python
# Workflow
x_rv = pt.random.poisson(2)
cens_x_rv = pt.clip(x_rv, 1, 4)
cens_x_vv = cens_x_rv.clone()
logprob = pt.sum(logp(cens_x_rv, cens_x_vv))
assert_no_rvs(logprob)
logp_fn = pytensor.function([cens_x_vv], logprob)
ref_scipy = st.poisson(2)
assert logp_fn(0) == -np.inf
assert logp_fn(5) == -np.inf
assert np.isclose(logp_fn(1), ref_scipy.logcdf(1))
assert np.isclose(logp_fn(4), np.logaddexp(ref_scipy.logsf(4), ref_scipy.logpmf(4)))
assert np.isclose(logp_fn(2), ref_scipy.logpmf(2))
```

## Next Steps


---

*Source: test_censoring.py:71 | Complexity: Intermediate | Last updated: 2026-05-18*