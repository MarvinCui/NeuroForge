# How To: Ifelse Mixture One Component

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test ifelse mixture one component

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.ifelse`
- `pytensor.link.numba`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.shape`
- `pytensor.tensor.subtensor`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.mixture`
- `pymc.logprob.rewriting`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign if_rv = pt.random.bernoulli(...)

```python
if_rv = pt.random.bernoulli(0.5, name='if')
```

**Verification:**
```python
assert_no_rvs(mix_logp)
```

### Step 2: Assign scale_rv = pt.random.halfnormal(...)

```python
scale_rv = pt.random.halfnormal(name='scale')
```

### Step 3: Assign comp_then = pt.random.normal(...)

```python
comp_then = pt.random.normal(0, scale_rv, size=(2,), name='comp_then')
```

### Step 4: Assign comp_else = pt.random.halfnormal(...)

```python
comp_else = pt.random.halfnormal(0, scale_rv, size=(4,), name='comp_else')
```

### Step 5: Assign mix_rv = ifelse(...)

```python
mix_rv = ifelse(if_rv, comp_then, comp_else, name='mix')
```

### Step 6: Assign if_vv = if_rv.clone(...)

```python
if_vv = if_rv.clone()
```

### Step 7: Assign scale_vv = scale_rv.clone(...)

```python
scale_vv = scale_rv.clone()
```

### Step 8: Assign mix_vv = mix_rv.clone(...)

```python
mix_vv = mix_rv.clone()
```

### Step 9: Assign mix_logp = value

```python
mix_logp = conditional_logp({if_rv: if_vv, scale_rv: scale_vv, mix_rv: mix_vv})[mix_vv]
```

### Step 10: Call assert_no_rvs()

```python
assert_no_rvs(mix_logp)
```

### Step 11: Assign fn = function(...)

```python
fn = function([if_vv, scale_vv, mix_vv], mix_logp)
```

### Step 12: Assign scale_vv_test = 0.75

```python
scale_vv_test = 0.75
```

### Step 13: Assign mix_vv_test = value

```python
mix_vv_test = np.r_[1.0, 2.5]
```

### Step 14: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(fn(1, scale_vv_test, mix_vv_test), sp.norm(0, scale_vv_test).logpdf(mix_vv_test))
```

### Step 15: Assign mix_vv_test = value

```python
mix_vv_test = np.r_[1.0, 2.5, 3.5, 4.0]
```

### Step 16: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(fn(0, scale_vv_test, mix_vv_test), sp.halfnorm(0, scale_vv_test).logpdf(mix_vv_test))
```


## Complete Example

```python
# Workflow
if_rv = pt.random.bernoulli(0.5, name='if')
scale_rv = pt.random.halfnormal(name='scale')
comp_then = pt.random.normal(0, scale_rv, size=(2,), name='comp_then')
comp_else = pt.random.halfnormal(0, scale_rv, size=(4,), name='comp_else')
mix_rv = ifelse(if_rv, comp_then, comp_else, name='mix')
if_vv = if_rv.clone()
scale_vv = scale_rv.clone()
mix_vv = mix_rv.clone()
mix_logp = conditional_logp({if_rv: if_vv, scale_rv: scale_vv, mix_rv: mix_vv})[mix_vv]
assert_no_rvs(mix_logp)
fn = function([if_vv, scale_vv, mix_vv], mix_logp)
scale_vv_test = 0.75
mix_vv_test = np.r_[1.0, 2.5]
np.testing.assert_array_almost_equal(fn(1, scale_vv_test, mix_vv_test), sp.norm(0, scale_vv_test).logpdf(mix_vv_test))
mix_vv_test = np.r_[1.0, 2.5, 3.5, 4.0]
np.testing.assert_array_almost_equal(fn(0, scale_vv_test, mix_vv_test), sp.halfnorm(0, scale_vv_test).logpdf(mix_vv_test))
```

## Next Steps


---

*Source: test_mixture.py:987 | Complexity: Advanced | Last updated: 2026-05-18*