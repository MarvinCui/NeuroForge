# How To: Log Transform Rv

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test log transform rv

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.lognormal(...)

```python
base_rv = pt.random.lognormal(0, 1, size=2, name='base_rv')
```

### Step 2: Assign y_rv = pt.log(...)

```python
y_rv = pt.log(base_rv)
```

### Step 3: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Assign logprob = logp(...)

```python
logprob = logp(y_rv, y_vv)
```

### Step 6: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([y_vv], logprob)
```

### Step 7: Assign y_val = value

```python
y_val = [0.1, 0.3]
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(y_val), sp.stats.norm().logpdf(y_val))
```


## Complete Example

```python
# Workflow
base_rv = pt.random.lognormal(0, 1, size=2, name='base_rv')
y_rv = pt.log(base_rv)
y_rv.name = 'y'
y_vv = y_rv.clone()
logprob = logp(y_rv, y_vv)
logp_fn = pytensor.function([y_vv], logprob)
y_val = [0.1, 0.3]
np.testing.assert_allclose(logp_fn(y_val), sp.stats.norm().logpdf(y_val))
```

## Next Steps


---

*Source: test_transforms.py:233 | Complexity: Advanced | Last updated: 2026-05-18*