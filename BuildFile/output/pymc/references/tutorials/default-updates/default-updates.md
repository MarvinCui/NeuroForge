# How To: Default Updates

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default updates

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

### Step 1: Assign mask = np.array(...)

```python
mask = np.array([True, True, False])
```

**Verification:**
```python
assert np.all(draws_obs_rv[0] != draws_obs_rv[1])
```

### Step 2: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist(shape=(3,))
```

**Verification:**
```python
assert np.all(draws_unobs_rv[0] != draws_unobs_rv[1])
```

### Step 3: Assign unknown = create_partial_observed_rv(...)

```python
(obs_rv, _), (unobs_rv, _), joined_rv = create_partial_observed_rv(rv, mask)
```

**Verification:**
```python
assert np.all(draws_joined_rv[0] != draws_joined_rv[1])
```

### Step 4: Assign unknown = pm.draw(...)

```python
draws_obs_rv, draws_unobs_rv, draws_joined_rv = pm.draw([obs_rv, unobs_rv, joined_rv], draws=2)
```

**Verification:**
```python
assert np.all(draws_obs_rv[0] != draws_obs_rv[1])
```


## Complete Example

```python
# Workflow
mask = np.array([True, True, False])
rv = pm.Normal.dist(shape=(3,))
(obs_rv, _), (unobs_rv, _), joined_rv = create_partial_observed_rv(rv, mask)
draws_obs_rv, draws_unobs_rv, draws_joined_rv = pm.draw([obs_rv, unobs_rv, joined_rv], draws=2)
assert np.all(draws_obs_rv[0] != draws_obs_rv[1])
assert np.all(draws_unobs_rv[0] != draws_unobs_rv[1])
assert np.all(draws_joined_rv[0] != draws_joined_rv[1])
```

## Next Steps


---

*Source: test_distribution.py:577 | Complexity: Intermediate | Last updated: 2026-05-18*