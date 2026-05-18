# How To: Recreate With Different Rng Inputs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can recreate a SymbolicRandomVariable with new RNG inputs.

Related to https://github.com/pymc-devs/pytensor/issues/473

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

### Step 1: 'Test that we can recreate a SymbolicRandomVariable with new RNG inputs.\n\n        Related to https://github.com/pymc-devs/pytensor/issues/473\n        '

```python
'Test that we can recreate a SymbolicRandomVariable with new RNG inputs.\n\n        Related to https://github.com/pymc-devs/pytensor/issues/473\n        '
```

**Verification:**
```python
assert op.update(x.owner) == {rng: next_rng}
```

### Step 2: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

**Verification:**
```python
assert op.update(new_x.owner) == {new_rng: new_next_rng}
```

### Step 3: Assign dummy_rng = rng.type(...)

```python
dummy_rng = rng.type()
```

### Step 4: Assign unknown = value

```python
dummy_next_rng, dummy_x = pt.random.normal(rng=dummy_rng).owner.outputs
```

### Step 5: Assign op = SymbolicRandomVariable(...)

```python
op = SymbolicRandomVariable([dummy_rng], [dummy_next_rng, dummy_x], ndim_supp=0)
```

### Step 6: Assign unknown = op(...)

```python
next_rng, x = op(rng)
```

**Verification:**
```python
assert op.update(x.owner) == {rng: next_rng}
```

### Step 7: Assign new_rng = pytensor.shared(...)

```python
new_rng = pytensor.shared(np.random.default_rng())
```

### Step 8: Assign inputs = x.owner.inputs.copy(...)

```python
inputs = x.owner.inputs.copy()
```

### Step 9: Assign unknown = new_rng

```python
inputs[0] = new_rng
```

### Step 10: Assign unknown = x.owner.op(...)

```python
new_next_rng, new_x = x.owner.op(*inputs)
```

**Verification:**
```python
assert op.update(new_x.owner) == {new_rng: new_next_rng}
```


## Complete Example

```python
# Workflow
'Test that we can recreate a SymbolicRandomVariable with new RNG inputs.\n\n        Related to https://github.com/pymc-devs/pytensor/issues/473\n        '
rng = pytensor.shared(np.random.default_rng())
dummy_rng = rng.type()
dummy_next_rng, dummy_x = pt.random.normal(rng=dummy_rng).owner.outputs
op = SymbolicRandomVariable([dummy_rng], [dummy_next_rng, dummy_x], ndim_supp=0)
next_rng, x = op(rng)
assert op.update(x.owner) == {rng: next_rng}
new_rng = pytensor.shared(np.random.default_rng())
inputs = x.owner.inputs.copy()
inputs[0] = new_rng
new_next_rng, new_x = x.owner.op(*inputs)
assert op.update(new_x.owner) == {new_rng: new_next_rng}
```

## Next Steps


---

*Source: test_distribution.py:190 | Complexity: Advanced | Last updated: 2026-05-18*