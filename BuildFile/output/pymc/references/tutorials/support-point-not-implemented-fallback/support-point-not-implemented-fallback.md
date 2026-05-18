# How To: Support Point Not Implemented Fallback

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test support point not implemented fallback

## Prerequisites

**Required Modules:**
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.builders`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.initial_point`


## Step-by-Step Guide

### Step 1: Assign name = 'my_normal'

```python
name = 'my_normal'
```

**Verification:**
```python
assert np.isclose(res['x'], np.pi)
```

### Step 2: Assign signature = '(),()->()'

```python
signature = '(),()->()'
```

### Step 3: Assign dtype = 'floatX'

```python
dtype = 'floatX'
```

### Step 4: Assign rv_op = MyNormalRV(...)

```python
rv_op = MyNormalRV()
```

### Step 5: Assign x = MyNormalDistribution(...)

```python
x = MyNormalDistribution('x', 0, 1, initval='support_point')
```

### Step 6: Assign res = m.initial_point(...)

```python
res = m.initial_point()
```


## Complete Example

```python
# Workflow
class MyNormalRV(RandomVariable):
    name = 'my_normal'
    signature = '(),()->()'
    dtype = 'floatX'

    @classmethod
    def rng_fn(cls, rng, mu, sigma, size):
        return np.pi

class MyNormalDistribution(pm.Normal):
    rv_op = MyNormalRV()
with pm.Model() as m:
    x = MyNormalDistribution('x', 0, 1, initval='support_point')
with pytest.warns(UserWarning, match='Support point not defined for variable x of type MyNormalRV'):
    res = m.initial_point()
assert np.isclose(res['x'], np.pi)
```

## Next Steps


---

*Source: test_initial_point.py:283 | Complexity: Intermediate | Last updated: 2026-05-18*