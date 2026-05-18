# How To: Discrete Rv Comparison Bitwise

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test discrete rv comparison bitwise

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: inputs, comparison_op, exp_logp_true, exp_logp_false
```

## Step-by-Step Guide

### Step 1: Assign cens_x_rv = comparison_op(...)

```python
cens_x_rv = comparison_op(*inputs)
```

**Verification:**
```python
assert_no_rvs(logprob)
```

### Step 2: Assign cens_x_vv = cens_x_rv.clone(...)

```python
cens_x_vv = cens_x_rv.clone()
```

**Verification:**
```python
assert np.isclose(logp_fn(1), exp_logp_true(3))
```

### Step 3: Assign logprob = logp(...)

```python
logprob = logp(cens_x_rv, cens_x_vv)
```

**Verification:**
```python
assert np.isclose(logp_fn(0), exp_logp_false(3))
```

### Step 4: Call assert_no_rvs()

```python
assert_no_rvs(logprob)
```

**Verification:**
```python
assert_no_rvs(logprob_not)
```

### Step 5: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([cens_x_vv], logprob)
```

**Verification:**
```python
assert np.isclose(logp_fn_not(1), exp_logp_false(3))
```

### Step 6: Assign bitwise_rv = pt.bitwise_not(...)

```python
bitwise_rv = pt.bitwise_not(comparison_op(*inputs))
```

**Verification:**
```python
assert np.isclose(logp_fn_not(0), exp_logp_true(3))
```

### Step 7: Assign bitwise_vv = bitwise_rv.clone(...)

```python
bitwise_vv = bitwise_rv.clone()
```

### Step 8: Assign logprob_not = logp(...)

```python
logprob_not = logp(bitwise_rv, bitwise_vv)
```

### Step 9: Call assert_no_rvs()

```python
assert_no_rvs(logprob_not)
```

### Step 10: Assign logp_fn_not = pytensor.function(...)

```python
logp_fn_not = pytensor.function([bitwise_vv], logprob_not)
```

**Verification:**
```python
assert np.isclose(logp_fn_not(1), exp_logp_false(3))
```


## Complete Example

```python
# Setup
# Fixtures: inputs, comparison_op, exp_logp_true, exp_logp_false

# Workflow
cens_x_rv = comparison_op(*inputs)
cens_x_vv = cens_x_rv.clone()
logprob = logp(cens_x_rv, cens_x_vv)
assert_no_rvs(logprob)
logp_fn = pytensor.function([cens_x_vv], logprob)
assert np.isclose(logp_fn(1), exp_logp_true(3))
assert np.isclose(logp_fn(0), exp_logp_false(3))
bitwise_rv = pt.bitwise_not(comparison_op(*inputs))
bitwise_vv = bitwise_rv.clone()
logprob_not = logp(bitwise_rv, bitwise_vv)
assert_no_rvs(logprob_not)
logp_fn_not = pytensor.function([bitwise_vv], logprob_not)
assert np.isclose(logp_fn_not(1), exp_logp_false(3))
assert np.isclose(logp_fn_not(0), exp_logp_true(3))
```

## Next Steps


---

*Source: test_binary.py:101 | Complexity: Advanced | Last updated: 2026-05-18*