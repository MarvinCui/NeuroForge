# How To: Change Dist Size None

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test change dist size none

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

### Step 1: Assign size = NoneConst

```python
size = NoneConst
```

**Verification:**
```python
assert rv.type.shape == ()
```

### Step 2: Assign rv = TestRV.rv_op(...)

```python
rv = TestRV.rv_op(size=size)
```

**Verification:**
```python
assert resized_rv.type.shape == (5,)
```

### Step 3: Assign resized_rv = change_dist_size(...)

```python
resized_rv = change_dist_size(rv, new_size=5)
```

**Verification:**
```python
assert resized_rv.type.shape == (5,)
```

### Step 4: Assign resized_rv = change_dist_size(...)

```python
resized_rv = change_dist_size(rv, new_size=5, expand=True)
```

**Verification:**
```python
assert resized_rv.type.shape == (5,)
```

### Step 5: Assign extended_signature = '[rng],[size]->[rng],(n)'

```python
extended_signature = '[rng],[size]->[rng],(n)'
```

### Step 6: Assign rng = normalize_rng_param(...)

```python
rng = normalize_rng_param(rng)
```

### Step 7: Assign size = normalize_size_param(...)

```python
size = normalize_size_param(size)
```

### Step 8: Assign unknown = value

```python
next_rng, draws = Normal.dist(size=size, rng=rng).owner.outputs
```


## Complete Example

```python
# Workflow
class TestRV(SymbolicRandomVariable):
    extended_signature = '[rng],[size]->[rng],(n)'

    @classmethod
    def rv_op(cls, size=None, rng=None):
        rng = normalize_rng_param(rng)
        size = normalize_size_param(size)
        next_rng, draws = Normal.dist(size=size, rng=rng).owner.outputs
        return cls(inputs=[rng, size], outputs=[next_rng, draws])(rng, size)
size = NoneConst
rv = TestRV.rv_op(size=size)
assert rv.type.shape == ()
resized_rv = change_dist_size(rv, new_size=5)
assert resized_rv.type.shape == (5,)
resized_rv = change_dist_size(rv, new_size=5, expand=True)
assert resized_rv.type.shape == (5,)
```

## Next Steps


---

*Source: test_distribution.py:216 | Complexity: Advanced | Last updated: 2026-05-18*