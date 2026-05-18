# How To: Multivariate Constant Mask Unseparable

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivariate constant mask unseparable

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

### Step 1: Assign mask = pt.constant(...)

```python
mask = pt.constant(np.array([[True, True, False, False]]))
```

**Verification:**
```python
assert isinstance(obs_rv.owner.op, PartialObservedRV)
```

### Step 2: Assign obs_data = np.array(...)

```python
obs_data = np.array([[0.1, 0.4, 0.1, 0.4]])
```

**Verification:**
```python
assert isinstance(unobs_rv.owner.op, PartialObservedRV)
```

### Step 3: Assign unobs_data = np.array(...)

```python
unobs_data = np.array([[0.4, 0.1, 0.4, 0.1]])
```

**Verification:**
```python
assert tuple(obs_rv.shape.eval()) == (2,)
```

### Step 4: Assign rv = pm.Dirichlet.dist(...)

```python
rv = pm.Dirichlet.dist([1, 2, 3, 4], shape=(1, 4))
```

**Verification:**
```python
assert tuple(unobs_rv.shape.eval()) == (2,)
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

### Step 7: Assign unknown = pytensor.function(...)

```python
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
```

### Step 8: Assign expected_logp = pm.logp.eval(...)

```python
expected_logp = pm.logp(rv, [[0.1, 0.4, 0.4, 0.1]]).eval()
```

### Step 9: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(obs_logp, expected_logp)
```

### Step 10: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(unobs_logp, [])
```


## Complete Example

```python
# Workflow
mask = pt.constant(np.array([[True, True, False, False]]))
obs_data = np.array([[0.1, 0.4, 0.1, 0.4]])
unobs_data = np.array([[0.4, 0.1, 0.4, 0.1]])
rv = pm.Dirichlet.dist([1, 2, 3, 4], shape=(1, 4))
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
assert isinstance(obs_rv.owner.op, PartialObservedRV)
assert isinstance(unobs_rv.owner.op, PartialObservedRV)
assert tuple(obs_rv.shape.eval()) == (2,)
assert tuple(unobs_rv.shape.eval()) == (2,)
assert tuple(joined_rv.shape.eval()) == (1, 4)
logp = conditional_logp({obs_rv: pt.as_tensor(obs_data)[obs_mask], unobs_rv: pt.as_tensor(unobs_data)[unobs_mask]})
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
expected_logp = pm.logp(rv, [[0.1, 0.4, 0.4, 0.1]]).eval()
np.testing.assert_almost_equal(obs_logp, expected_logp)
np.testing.assert_array_equal(unobs_logp, [])
```

## Next Steps


---

*Source: test_distribution.py:420 | Complexity: Advanced | Last updated: 2026-05-18*