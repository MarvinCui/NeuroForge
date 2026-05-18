# How To: Switch Mixture Constant Branch Broadcast Ok

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test switch mixture constant branch broadcast ok

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

### Step 1: Assign t = pt.arange(...)

```python
t = pt.arange(10)
```

**Verification:**
```python
assert np.isneginf(bad_const[0])
```

### Step 2: Assign p = pt.as_tensor(...)

```python
p = pt.as_tensor(np.array([0.5, 0.5], dtype=pytensor.config.floatX))
```

**Verification:**
```python
assert np.isneginf(bad_dirac[0])
```

### Step 3: Assign cat = pt.random.categorical(...)

```python
cat = pt.random.categorical(p=p, size=(10,))
```

### Step 4: Assign cat_fixed_const = pt.where(...)

```python
cat_fixed_const = pt.where(t > 5, cat, -1)
```

### Step 5: Assign dirac_branch = dirac_delta(...)

```python
dirac_branch = dirac_delta(pt.full_like(t, -1, dtype=cat.dtype))
```

### Step 6: Assign cat_fixed_dirac = pt.where(...)

```python
cat_fixed_dirac = pt.where(t > 5, cat, dirac_branch)
```

### Step 7: Assign vv_const = cat_fixed_const.clone(...)

```python
vv_const = cat_fixed_const.clone()
```

### Step 8: Assign vv_dirac = cat_fixed_dirac.clone(...)

```python
vv_dirac = cat_fixed_dirac.clone()
```

### Step 9: Assign logp_const = logp(...)

```python
logp_const = logp(cat_fixed_const, vv_const)
```

### Step 10: Assign logp_dirac = logp(...)

```python
logp_dirac = logp(cat_fixed_dirac, vv_dirac)
```

### Step 11: Assign test_value = np.where.astype(...)

```python
test_value = np.where(np.arange(10) > 5, 0, -1).astype(vv_const.dtype)
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_const.eval({vv_const: test_value}), logp_dirac.eval({vv_dirac: test_value.astype(vv_dirac.dtype)}))
```

### Step 13: Assign bad_value = test_value.copy(...)

```python
bad_value = test_value.copy()
```

### Step 14: Assign unknown = 0

```python
bad_value[0] = 0
```

### Step 15: Assign bad_const = logp_const.eval(...)

```python
bad_const = logp_const.eval({vv_const: bad_value})
```

### Step 16: Assign bad_dirac = logp_dirac.eval(...)

```python
bad_dirac = logp_dirac.eval({vv_dirac: bad_value.astype(vv_dirac.dtype)})
```

**Verification:**
```python
assert np.isneginf(bad_const[0])
```


## Complete Example

```python
# Workflow
t = pt.arange(10)
p = pt.as_tensor(np.array([0.5, 0.5], dtype=pytensor.config.floatX))
cat = pt.random.categorical(p=p, size=(10,))
cat_fixed_const = pt.where(t > 5, cat, -1)
dirac_branch = dirac_delta(pt.full_like(t, -1, dtype=cat.dtype))
cat_fixed_dirac = pt.where(t > 5, cat, dirac_branch)
vv_const = cat_fixed_const.clone()
vv_dirac = cat_fixed_dirac.clone()
logp_const = logp(cat_fixed_const, vv_const)
logp_dirac = logp(cat_fixed_dirac, vv_dirac)
test_value = np.where(np.arange(10) > 5, 0, -1).astype(vv_const.dtype)
np.testing.assert_allclose(logp_const.eval({vv_const: test_value}), logp_dirac.eval({vv_dirac: test_value.astype(vv_dirac.dtype)}))
bad_value = test_value.copy()
bad_value[0] = 0
bad_const = logp_const.eval({vv_const: bad_value})
bad_dirac = logp_dirac.eval({vv_dirac: bad_value.astype(vv_dirac.dtype)})
assert np.isneginf(bad_const[0])
assert np.isneginf(bad_dirac[0])
```

## Next Steps


---

*Source: test_mixture.py:953 | Complexity: Advanced | Last updated: 2026-05-18*