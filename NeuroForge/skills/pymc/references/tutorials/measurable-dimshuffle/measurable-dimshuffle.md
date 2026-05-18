# How To: Measurable Dimshuffle

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test measurable dimshuffle

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.tensor.random.type`
- `scipy`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: ds_order, multivariate
```

## Step-by-Step Guide

### Step 1: Assign ds_rv = base_rv.dimshuffle(...)

```python
ds_rv = base_rv.dimshuffle(ds_order)
```

**Verification:**
```python
assert ds_logp_combined is not None
```

### Step 2: Assign base_vv = base_rv.clone(...)

```python
base_vv = base_rv.clone()
```

### Step 3: Assign ds_vv = ds_rv.clone(...)

```python
ds_vv = ds_rv.clone()
```

### Step 4: Assign ref_logp = logp.dimshuffle(...)

```python
ref_logp = logp(base_rv, base_vv).dimshuffle(logp_ds_order)
```

### Step 5: Assign ir_rewriter = logprob_rewrites_db.query(...)

```python
ir_rewriter = logprob_rewrites_db.query(RewriteDatabaseQuery(include=['basic']).excluding('dimshuffle_lift'))
```

### Step 6: Assign ds_logp = conditional_logp(...)

```python
ds_logp = conditional_logp({ds_rv: ds_vv}, ir_rewriter=ir_rewriter)
```

### Step 7: Assign ds_logp_combined = pt.add(...)

```python
ds_logp_combined = pt.add(*ds_logp.values())
```

**Verification:**
```python
assert ds_logp_combined is not None
```

### Step 8: Assign ref_logp_fn = pytensor.function(...)

```python
ref_logp_fn = pytensor.function([base_vv], ref_logp)
```

### Step 9: Assign ds_logp_fn = pytensor.function(...)

```python
ds_logp_fn = pytensor.function([ds_vv], ds_logp_combined)
```

### Step 10: Assign base_test_value = base_rv.eval(...)

```python
base_test_value = base_rv.eval()
```

### Step 11: Assign ds_test_value = pt.constant.dimshuffle.eval(...)

```python
ds_test_value = pt.constant(base_test_value).dimshuffle(ds_order).eval()
```

### Step 12: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(ref_logp_fn(base_test_value), ds_logp_fn(ds_test_value))
```

### Step 13: Assign base_rv = pt.random.dirichlet(...)

```python
base_rv = pt.random.dirichlet([1, 2, 3], size=(2, 1))
```

### Step 14: Assign base_rv = pt.exp(...)

```python
base_rv = pt.exp(pt.random.beta(1, 2, size=(2, 1, 3)))
```

### Step 15: Assign logp_ds_order = value

```python
logp_ds_order = [o for o in ds_order if o == 'x' or o < 2]
```

### Step 16: Assign logp_ds_order = ds_order

```python
logp_ds_order = ds_order
```


## Complete Example

```python
# Setup
# Fixtures: ds_order, multivariate

# Workflow
if multivariate:
    base_rv = pt.random.dirichlet([1, 2, 3], size=(2, 1))
else:
    base_rv = pt.exp(pt.random.beta(1, 2, size=(2, 1, 3)))
ds_rv = base_rv.dimshuffle(ds_order)
base_vv = base_rv.clone()
ds_vv = ds_rv.clone()
if multivariate:
    logp_ds_order = [o for o in ds_order if o == 'x' or o < 2]
else:
    logp_ds_order = ds_order
ref_logp = logp(base_rv, base_vv).dimshuffle(logp_ds_order)
ir_rewriter = logprob_rewrites_db.query(RewriteDatabaseQuery(include=['basic']).excluding('dimshuffle_lift'))
ds_logp = conditional_logp({ds_rv: ds_vv}, ir_rewriter=ir_rewriter)
ds_logp_combined = pt.add(*ds_logp.values())
assert ds_logp_combined is not None
ref_logp_fn = pytensor.function([base_vv], ref_logp)
ds_logp_fn = pytensor.function([ds_vv], ds_logp_combined)
base_test_value = base_rv.eval()
ds_test_value = pt.constant(base_test_value).dimshuffle(ds_order).eval()
np.testing.assert_array_equal(ref_logp_fn(base_test_value), ds_logp_fn(ds_test_value))
```

## Next Steps


---

*Source: test_tensor.py:382 | Complexity: Advanced | Last updated: 2026-05-18*