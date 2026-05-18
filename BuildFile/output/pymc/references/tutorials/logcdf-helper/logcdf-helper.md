# How To: Logcdf Helper

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logcdf helper

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.scalar`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pytensor.graph.traversal`
- `pytensor.scalar.math`
- `pytensor.tensor.elemwise`


## Step-by-Step Guide

### Step 1: Assign value = pt.vector(...)

```python
value = pt.vector('value')
```

### Step 2: Assign x = pm.Normal.dist(...)

```python
x = pm.Normal.dist(0, 1)
```

### Step 3: Assign x_logcdf = _logcdf_helper(...)

```python
x_logcdf = _logcdf_helper(x, value)
```

### Step 4: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(x_logcdf.eval({value: [0, 1]}), sp.norm(0, 1).logcdf([0, 1]))
```

### Step 5: Assign x_logcdf = _logcdf_helper(...)

```python
x_logcdf = _logcdf_helper(x, [0, 1])
```

### Step 6: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(x_logcdf.eval(), sp.norm(0, 1).logcdf([0, 1]))
```


## Complete Example

```python
# Workflow
value = pt.vector('value')
x = pm.Normal.dist(0, 1)
x_logcdf = _logcdf_helper(x, value)
np.testing.assert_almost_equal(x_logcdf.eval({value: [0, 1]}), sp.norm(0, 1).logcdf([0, 1]))
x_logcdf = _logcdf_helper(x, [0, 1])
np.testing.assert_almost_equal(x_logcdf.eval(), sp.norm(0, 1).logcdf([0, 1]))
```

## Next Steps


---

*Source: test_abstract.py:72 | Complexity: Intermediate | Last updated: 2026-05-18*