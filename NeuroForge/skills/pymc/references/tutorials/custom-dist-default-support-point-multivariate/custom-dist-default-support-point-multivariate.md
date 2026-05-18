# How To: Custom Dist Default Support Point Multivariate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test custom dist default support point multivariate

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `numpy`
- `pytensor`
- `pytensor`
- `pytensor.graph`
- `scipy`
- `pymc.distributions`
- `pymc.distributions.custom`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling`
- `pymc.step_methods`
- `pymc.testing`
- `numpy`

**Setup Required:**
```python
# Fixtures: with_random, size
```

## Step-by-Step Guide

### Step 1: Assign random = _random

```python
random = _random
```

**Verification:**
```python
assert isinstance(a.owner.op, CustomDistRV)
```

### Step 2: Assign random = None

```python
random = None
```

**Verification:**
```python
assert evaled_support_point.shape == (*to_tuple(size), 5)
```

### Step 3: Assign mu = Normal(...)

```python
mu = Normal('mu', size=5)
```

**Verification:**
```python
assert np.all(evaled_support_point == 0)
```

### Step 4: Assign a = CustomDist(...)

```python
a = CustomDist('a', mu, random=random, signature='(n)->(n)', size=size)
```

### Step 5: Assign evaled_support_point = support_point.eval(...)

```python
evaled_support_point = support_point(a).eval()
```

**Verification:**
```python
assert evaled_support_point.shape == (*to_tuple(size), 5)
```


## Complete Example

```python
# Setup
# Fixtures: with_random, size

# Workflow
def _random(mu, rng=None, size=None):
    return rng.normal(mu, scale=1, size=to_tuple(size) + mu.shape)
if with_random:
    random = _random
else:
    random = None
with Model():
    mu = Normal('mu', size=5)
    a = CustomDist('a', mu, random=random, signature='(n)->(n)', size=size)
assert isinstance(a.owner.op, CustomDistRV)
if with_random:
    evaled_support_point = support_point(a).eval()
    assert evaled_support_point.shape == (*to_tuple(size), 5)
    assert np.all(evaled_support_point == 0)
```

## Next Steps


---

*Source: test_custom.py:248 | Complexity: Intermediate | Last updated: 2026-05-18*