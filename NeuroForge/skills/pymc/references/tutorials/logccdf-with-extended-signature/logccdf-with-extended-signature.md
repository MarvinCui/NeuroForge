# How To: Logccdf With Extended Signature

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test logccdf registration for SymbolicRandomVariable with extended_signature.

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

### Step 1: 'Test logccdf registration for SymbolicRandomVariable with extended_signature.'

```python
'Test logccdf registration for SymbolicRandomVariable with extended_signature.'
```

### Step 2: Assign rv = TestDistWithLogccdf.dist(...)

```python
rv = TestDistWithLogccdf.dist(0, 1)
```

### Step 3: Assign result = pm.logccdf.eval(...)

```python
result = pm.logccdf(rv, 0.5).eval()
```

### Step 4: Assign expected = st.norm.logsf(...)

```python
expected = st.norm(0, 1).logsf(0.5)
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(result, expected)
```

### Step 6: Assign rv_type = type(...)

```python
rv_type = type('TestRVWithLogccdf', (SymbolicRandomVariable,), {'extended_signature': '[rng],[size],(),()->[rng],()'})
```

### Step 7: Assign mu = pt.as_tensor(...)

```python
mu = pt.as_tensor(mu)
```

### Step 8: Assign sigma = pt.as_tensor(...)

```python
sigma = pt.as_tensor(sigma)
```

### Step 9: Assign rng = normalize_rng_param(...)

```python
rng = normalize_rng_param(rng)
```

### Step 10: Assign size = normalize_size_param(...)

```python
size = normalize_size_param(size)
```

### Step 11: Assign unknown = value

```python
next_rng, draws = Normal.dist(mu, sigma, size=size, rng=rng).owner.outputs
```


## Complete Example

```python
# Workflow
'Test logccdf registration for SymbolicRandomVariable with extended_signature.'
from pymc.distributions.dist_math import normal_lccdf
from pymc.distributions.distribution import Distribution

class TestDistWithLogccdf(Distribution):
    rv_type = type('TestRVWithLogccdf', (SymbolicRandomVariable,), {'extended_signature': '[rng],[size],(),()->[rng],()'})

    @classmethod
    def dist(cls, mu, sigma, **kwargs):
        mu = pt.as_tensor(mu)
        sigma = pt.as_tensor(sigma)
        return super().dist([mu, sigma], **kwargs)

    @classmethod
    def rv_op(cls, mu, sigma, size=None, rng=None):
        rng = normalize_rng_param(rng)
        size = normalize_size_param(size)
        next_rng, draws = Normal.dist(mu, sigma, size=size, rng=rng).owner.outputs
        return cls.rv_type(inputs=[rng, size, mu, sigma], outputs=[next_rng, draws], ndim_supp=0)(rng, size, mu, sigma)

    def logccdf(value, mu, sigma):
        return normal_lccdf(mu, sigma, value)
rv = TestDistWithLogccdf.dist(0, 1)
result = pm.logccdf(rv, 0.5).eval()
expected = st.norm(0, 1).logsf(0.5)
npt.assert_allclose(result, expected)
```

## Next Steps


---

*Source: test_distribution.py:237 | Complexity: Advanced | Last updated: 2026-05-18*