# How To: Random Multiple Rngs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random multiple rngs

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign customdist = CustomDist.dist(...)

```python
customdist = CustomDist.dist(0.5, 10.0, dist=custom_dist, size=(10,))
```

**Verification:**
```python
assert isinstance(customdist.owner.op, CustomSymbolicDistRV)
```

### Step 2: Assign node = value

```python
node = customdist.owner
```

**Verification:**
```python
assert len(node.inputs) == 5
```

### Step 3: Assign draws = draw(...)

```python
draws = draw(customdist, draws=2, random_seed=123)
```

**Verification:**
```python
assert len(node.outputs) == 3
```

### Step 4: Assign idx = Bernoulli.dist(...)

```python
idx = Bernoulli.dist(p=p)
```

**Verification:**
```python
assert len(node.op.update(node)) == 2
```

### Step 5: Assign comps = value

```python
comps = Normal.dist([-sigma, sigma], 0.1, size=(*size, 2)).T
```

**Verification:**
```python
assert np.unique(draws).size == 20
```

### Step 6: Assign size = pt.broadcast_shape(...)

```python
size = pt.broadcast_shape(p, sigma)
```


## Complete Example

```python
# Workflow
def custom_dist(p, sigma, size):
    idx = Bernoulli.dist(p=p)
    if rv_size_is_none(size):
        size = pt.broadcast_shape(p, sigma)
    comps = Normal.dist([-sigma, sigma], 0.1, size=(*size, 2)).T
    return comps[idx]
customdist = CustomDist.dist(0.5, 10.0, dist=custom_dist, size=(10,))
assert isinstance(customdist.owner.op, CustomSymbolicDistRV)
node = customdist.owner
assert len(node.inputs) == 5
assert len(node.outputs) == 3
assert len(node.op.update(node)) == 2
draws = draw(customdist, draws=2, random_seed=123)
assert np.unique(draws).size == 20
```

## Next Steps


---

*Source: test_custom.py:444 | Complexity: Intermediate | Last updated: 2026-05-18*