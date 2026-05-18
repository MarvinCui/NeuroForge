# How To: Multivariate Shared Mask Separable

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivariate shared mask separable

## Prerequisites

**Required Modules:**
- `sys`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor`
- `pytensor.tensor`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.logprob.basic`
- `pymc.pytensorf`
- `pymc.testing`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`


## Step-by-Step Guide

### Step 1: Assign mask = shared(...)

```python
mask = shared(np.array([True]))
```

**Verification:**
```python
assert isinstance(obs_rv.owner.op, pm.Dirichlet)
```

### Step 2: Assign obs_data = np.array(...)

```python
obs_data = np.array([[0.1, 0.4, 0.1, 0.4]])
```

**Verification:**
```python
assert isinstance(unobs_rv.owner.op, pm.Dirichlet)
```

### Step 3: Assign unobs_data = np.array(...)

```python
unobs_data = np.array([[0.4, 0.1, 0.4, 0.1]])
```

**Verification:**
```python
assert tuple(obs_rv.shape.eval()) == (0, 4)
```

### Step 4: Assign rv = pm.Dirichlet.dist(...)

```python
rv = pm.Dirichlet.dist([1, 2, 3, 4], shape=(1, 4))
```

**Verification:**
```python
assert tuple(unobs_rv.shape.eval()) == (1, 4)
```

### Step 5: Assign unknown = create_partial_observed_rv(...)

```python
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
```

**Verification:**
```python
assert tuple(joined_rv.shape.eval()) == (1, 4)
```

### Step 6: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({obs_rv: pt.as_tensor(obs_data)[obs_mask], unobs_rv: pt.as_tensor(unobs_data)[unobs_mask]})
```

**Verification:**
```python
assert tuple(obs_rv.shape.eval()) == (1, 4)
```

### Step 7: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([], list(logp.values()))
```

**Verification:**
```python
assert tuple(unobs_rv.shape.eval()) == (0, 4)
```

### Step 8: Assign unknown = logp_fn(...)

```python
obs_logp, unobs_logp = logp_fn()
```

**Verification:**
```python
assert not np.isclose(expected_logp, new_expected_logp)
```

### Step 9: Assign expected_logp = pm.logp.eval(...)

```python
expected_logp = pm.logp(rv, unobs_data).eval()
```

### Step 10: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(obs_logp, [])
```

### Step 11: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(unobs_logp, expected_logp)
```

### Step 12: Call mask.set_value()

```python
mask.set_value(np.array([False]))
```

**Verification:**
```python
assert tuple(obs_rv.shape.eval()) == (1, 4)
```

### Step 13: Assign new_expected_logp = pm.logp.eval(...)

```python
new_expected_logp = pm.logp(rv, obs_data).eval()
```

**Verification:**
```python
assert not np.isclose(expected_logp, new_expected_logp)
```

### Step 14: Assign unknown = logp_fn(...)

```python
obs_logp, unobs_logp = logp_fn()
```

### Step 15: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(obs_logp, new_expected_logp)
```

### Step 16: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(unobs_logp, [])
```


## Complete Example

```python
# Workflow
mask = shared(np.array([True]))
obs_data = np.array([[0.1, 0.4, 0.1, 0.4]])
unobs_data = np.array([[0.4, 0.1, 0.4, 0.1]])
rv = pm.Dirichlet.dist([1, 2, 3, 4], shape=(1, 4))
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
assert isinstance(obs_rv.owner.op, pm.Dirichlet)
assert isinstance(unobs_rv.owner.op, pm.Dirichlet)
assert tuple(obs_rv.shape.eval()) == (0, 4)
assert tuple(unobs_rv.shape.eval()) == (1, 4)
assert tuple(joined_rv.shape.eval()) == (1, 4)
logp = conditional_logp({obs_rv: pt.as_tensor(obs_data)[obs_mask], unobs_rv: pt.as_tensor(unobs_data)[unobs_mask]})
logp_fn = pytensor.function([], list(logp.values()))
obs_logp, unobs_logp = logp_fn()
expected_logp = pm.logp(rv, unobs_data).eval()
np.testing.assert_almost_equal(obs_logp, [])
np.testing.assert_almost_equal(unobs_logp, expected_logp)
mask.set_value(np.array([False]))
assert tuple(obs_rv.shape.eval()) == (1, 4)
assert tuple(unobs_rv.shape.eval()) == (0, 4)
new_expected_logp = pm.logp(rv, obs_data).eval()
assert not np.isclose(expected_logp, new_expected_logp)
obs_logp, unobs_logp = logp_fn()
np.testing.assert_almost_equal(obs_logp, new_expected_logp)
np.testing.assert_array_equal(unobs_logp, [])
```

## Next Steps


---

*Source: test_distribution.py:451 | Complexity: Advanced | Last updated: 2026-05-18*