# How To: Logcdf Inference

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logcdf inference

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

### Step 1: Assign mu = 1

```python
mu = 1
```

### Step 2: Assign sigma = 1.25

```python
sigma = 1.25
```

### Step 3: Assign test_value = 0.9

```python
test_value = 0.9
```

### Step 4: Assign custom_lognormal = CustomDist.dist(...)

```python
custom_lognormal = CustomDist.dist(mu, sigma, dist=custom_dist)
```

### Step 5: Assign ref_lognormal = LogNormal.dist(...)

```python
ref_lognormal = LogNormal.dist(mu, sigma)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logcdf(custom_lognormal, test_value).eval(), logcdf(ref_lognormal, test_value).eval())
```


## Complete Example

```python
# Workflow
def custom_dist(mu, sigma, size):
    return pt.exp(Normal.dist(mu, sigma, size=size))
mu = 1
sigma = 1.25
test_value = 0.9
custom_lognormal = CustomDist.dist(mu, sigma, dist=custom_dist)
ref_lognormal = LogNormal.dist(mu, sigma)
np.testing.assert_allclose(logcdf(custom_lognormal, test_value).eval(), logcdf(ref_lognormal, test_value).eval())
```

## Next Steps


---

*Source: test_custom.py:428 | Complexity: Intermediate | Last updated: 2026-05-18*