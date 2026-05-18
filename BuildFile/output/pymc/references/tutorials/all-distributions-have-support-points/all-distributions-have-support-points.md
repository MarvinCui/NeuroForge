# How To: All Distributions Have Support Points

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test all distributions have support points

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

### Step 1: Assign dists = value

```python
dists = (getattr(dist_module, dist) for dist in dist_module.__all__)
```

### Step 2: Assign dists = value

```python
dists = (dist for dist in dists if isinstance(dist, DistributionMeta))
```

### Step 3: Assign generic_func = _support_point.dispatch(...)

```python
generic_func = _support_point.dispatch(object)
```

### Step 4: Assign missing_support_points = value

```python
missing_support_points = {dist for dist in dists if getattr(dist, 'rv_type', None) is not None and _support_point.dispatch(dist.rv_type) is generic_func}
```

### Step 5: Assign not_implemented = value

```python
not_implemented = {dist_module.timeseries.EulerMaruyama}
```

### Step 6: Assign unexpected_implemented = value

```python
unexpected_implemented = not_implemented - missing_support_points
```

### Step 7: Assign unexpected_not_implemented = value

```python
unexpected_not_implemented = missing_support_points - not_implemented
```


## Complete Example

```python
# Workflow
import pymc.distributions as dist_module
from pymc.distributions.distribution import DistributionMeta
dists = (getattr(dist_module, dist) for dist in dist_module.__all__)
dists = (dist for dist in dists if isinstance(dist, DistributionMeta))
generic_func = _support_point.dispatch(object)
missing_support_points = {dist for dist in dists if getattr(dist, 'rv_type', None) is not None and _support_point.dispatch(dist.rv_type) is generic_func}
missing_support_points -= {dist_module.Distribution, dist_module.Discrete, dist_module.Continuous, dist_module.CustomDist, dist_module.simulator.Simulator}
not_implemented = {dist_module.timeseries.EulerMaruyama}
unexpected_implemented = not_implemented - missing_support_points
if unexpected_implemented:
    raise Exception(f'Distributions {unexpected_implemented} have a `support_point` implemented. This test must be updated to expect this.')
unexpected_not_implemented = missing_support_points - not_implemented
if unexpected_not_implemented:
    raise NotImplementedError(f'Unexpected by this test, distributions {unexpected_not_implemented} do not have a `support_point` implementation. Either add a support_point or filter these distributions in this test.')
```

## Next Steps


---

*Source: test_distribution.py:87 | Complexity: Intermediate | Last updated: 2026-05-18*