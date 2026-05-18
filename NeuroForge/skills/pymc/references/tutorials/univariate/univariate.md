# How To: Univariate

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test univariate

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: symbolic_rv
```

## Step-by-Step Guide

### Step 1: Assign data = np.array(...)

```python
data = np.array([0.25, 0.5, 0.25])
```

**Verification:**
```python
assert isinstance(obs_rv.owner.op, PartialObservedRV)
```

### Step 2: Assign mask = np.array(...)

```python
mask = np.array([False, False, True])
```

**Verification:**
```python
assert isinstance(unobs_rv.owner.op, PartialObservedRV)
```

### Step 3: Assign rv = pm.Normal.dist(...)

```python
rv = pm.Normal.dist([1, 2, 3])
```

**Verification:**
```python
assert isinstance(obs_rv.owner.op, Normal)
```

### Step 4: Assign unknown = create_partial_observed_rv(...)

```python
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
```

**Verification:**
```python
assert isinstance(unobs_rv.owner.op, Normal)
```

### Step 5: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({obs_rv: pt.as_tensor(data[~mask]), unobs_rv: pt.as_tensor(data[mask])})
```

**Verification:**
```python
assert tuple(obs_rv.shape.eval()) == (2,)
```

### Step 6: Assign unknown = pytensor.function(...)

```python
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
```

**Verification:**
```python
assert tuple(unobs_rv.shape.eval()) == (1,)
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(obs_logp, st.norm([1, 2]).logpdf([0.25, 0.5]))
```

**Verification:**
```python
assert tuple(joined_rv.shape.eval()) == (3,)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(unobs_logp, st.norm([3]).logpdf([0.25]))
```

### Step 9: Assign rv = pm.Censored.dist(...)

```python
rv = pm.Censored.dist(rv, lower=-100, upper=100)
```

**Verification:**
```python
assert isinstance(obs_rv.owner.op, PartialObservedRV)
```


## Complete Example

```python
# Setup
# Fixtures: symbolic_rv

# Workflow
data = np.array([0.25, 0.5, 0.25])
mask = np.array([False, False, True])
rv = pm.Normal.dist([1, 2, 3])
if symbolic_rv:
    rv = pm.Censored.dist(rv, lower=-100, upper=100)
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
if symbolic_rv:
    assert isinstance(obs_rv.owner.op, PartialObservedRV)
    assert isinstance(unobs_rv.owner.op, PartialObservedRV)
else:
    assert isinstance(obs_rv.owner.op, Normal)
    assert isinstance(unobs_rv.owner.op, Normal)
assert tuple(obs_rv.shape.eval()) == (2,)
assert tuple(unobs_rv.shape.eval()) == (1,)
assert tuple(joined_rv.shape.eval()) == (3,)
logp = conditional_logp({obs_rv: pt.as_tensor(data[~mask]), unobs_rv: pt.as_tensor(data[mask])})
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
np.testing.assert_allclose(obs_logp, st.norm([1, 2]).logpdf([0.25, 0.5]))
np.testing.assert_allclose(unobs_logp, st.norm([3]).logpdf([0.25]))
```

## Next Steps


---

*Source: test_distribution.py:335 | Complexity: Advanced | Last updated: 2026-05-18*