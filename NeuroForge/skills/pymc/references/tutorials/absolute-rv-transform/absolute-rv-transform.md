# How To: Absolute Rv Transform

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test absolute rv transform

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`

**Setup Required:**
```python
# Fixtures: test_val
```

## Step-by-Step Guide

### Step 1: Assign x_rv = pt.abs(...)

```python
x_rv = pt.abs(pt.random.normal())
```

### Step 2: Assign y_rv = pt.random.halfnormal(...)

```python
y_rv = pt.random.halfnormal()
```

### Step 3: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Assign x_logp_fn = pytensor.function(...)

```python
x_logp_fn = pytensor.function([x_vv], logp(x_rv, x_vv))
```

### Step 6: Assign y_logp_fn = pytensor.function(...)

```python
y_logp_fn = pytensor.function([y_vv], logp(y_rv, y_vv))
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_logp_fn(test_val), y_logp_fn(test_val))
```

### Step 8: Call logcdf()

```python
logcdf(x_rv, x_vv)
```

### Step 9: Call icdf()

```python
icdf(x_rv, x_vv)
```


## Complete Example

```python
# Setup
# Fixtures: test_val

# Workflow
x_rv = pt.abs(pt.random.normal())
y_rv = pt.random.halfnormal()
x_vv = x_rv.clone()
y_vv = y_rv.clone()
x_logp_fn = pytensor.function([x_vv], logp(x_rv, x_vv))
with pytest.raises(NotImplementedError):
    logcdf(x_rv, x_vv)
with pytest.raises(NotImplementedError):
    icdf(x_rv, x_vv)
y_logp_fn = pytensor.function([y_vv], logp(y_rv, y_vv))
np.testing.assert_allclose(x_logp_fn(test_val), y_logp_fn(test_val))
```

## Next Steps


---

*Source: test_transforms.py:506 | Complexity: Advanced | Last updated: 2026-05-18*