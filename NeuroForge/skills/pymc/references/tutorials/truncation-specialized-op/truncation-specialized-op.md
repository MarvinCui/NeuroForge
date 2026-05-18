# How To: Truncation Specialized Op

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test truncation specialized op

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `pytensor.scalar`
- `pytensor.scan.op`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.type`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.distributions.truncated`
- `pymc.exceptions`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: shape_info
```

## Step-by-Step Guide

### Step 1: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

**Verification:**
```python
assert isinstance(xt.owner.op, TruncatedNormal.rv_type)
```

### Step 2: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(0, 10, rng=rng, name='x')
```

**Verification:**
```python
assert xt.shape.eval() == (100,)
```

### Step 3: Assign lower_upper = pt.stack(...)

```python
lower_upper = pt.stack(xt.owner.inputs[4:])
```

**Verification:**
```python
assert xt.owner.inputs[0] is not rng
```

### Step 4: Assign xt = Truncated(...)

```python
xt = Truncated('xt', dist=x, lower=5, upper=15, shape=(100,))
```

**Verification:**
```python
assert np.all(lower_upper.eval().squeeze() == [5, 15])
```

### Step 5: Assign xt = Truncated(...)

```python
xt = Truncated('xt', dist=x, lower=5, upper=15, dims=('dim',))
```

### Step 6: Assign xt = Truncated(...)

```python
xt = Truncated('xt', dist=x, lower=5, upper=15, observed=np.zeros(100))
```


## Complete Example

```python
# Setup
# Fixtures: shape_info

# Workflow
rng = pytensor.shared(np.random.default_rng())
x = pt.random.normal(0, 10, rng=rng, name='x')
with Model(coords={'dim': range(100)}) as m:
    if shape_info == 'shape':
        xt = Truncated('xt', dist=x, lower=5, upper=15, shape=(100,))
    elif shape_info == 'dims':
        xt = Truncated('xt', dist=x, lower=5, upper=15, dims=('dim',))
    elif shape_info == 'observed':
        xt = Truncated('xt', dist=x, lower=5, upper=15, observed=np.zeros(100))
    else:
        raise ValueError(f'Not a valid shape_info parametrization: {shape_info}')
assert isinstance(xt.owner.op, TruncatedNormal.rv_type)
assert xt.shape.eval() == (100,)
assert xt.owner.inputs[0] is not rng
lower_upper = pt.stack(xt.owner.inputs[4:])
assert np.all(lower_upper.eval().squeeze() == [5, 15])
```

## Next Steps


---

*Source: test_truncated.py:104 | Complexity: Intermediate | Last updated: 2026-05-18*