# How To: Chain Values

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test chain values

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.pytensorf`
- `pymc.testing`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign chain_tranf = tr.Chain(...)

```python
chain_tranf = tr.Chain([tr.logodds, tr.ordered])
```

**Verification:**
```python
assert_array_equal(np.diff(vals) >= 0, True)
```

### Step 2: Assign vals = get_values(...)

```python
vals = get_values(chain_tranf, Vector(R, 5), pt.vector, floatX(np.zeros(5)))
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(np.diff(vals) >= 0, True)
```


## Complete Example

```python
# Workflow
chain_tranf = tr.Chain([tr.logodds, tr.ordered])
vals = get_values(chain_tranf, Vector(R, 5), pt.vector, floatX(np.zeros(5)))
assert_array_equal(np.diff(vals) >= 0, True)
```

## Next Steps


---

*Source: test_transform.py:291 | Complexity: Beginner | Last updated: 2026-05-18*