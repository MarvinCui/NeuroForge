# How To: Draw Pytensor Function Kwargs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test draw pytensor function kwargs

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `arviz_base`
- `arviz_base.testing`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.tensor.variable`
- `scipy`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign sharedvar = pytensor.shared(...)

```python
sharedvar = pytensor.shared(0)
```

**Verification:**
```python
assert np.all(draws == np.arange(5))
```

### Step 2: Assign x = pm.DiracDelta.dist(...)

```python
x = pm.DiracDelta.dist(0.0)
```

### Step 3: Assign y = value

```python
y = x + sharedvar
```

### Step 4: Assign draws = pm.draw(...)

```python
draws = pm.draw(y, draws=5, mode=Mode('py'), updates={sharedvar: sharedvar + 1})
```

**Verification:**
```python
assert np.all(draws == np.arange(5))
```


## Complete Example

```python
# Workflow
sharedvar = pytensor.shared(0)
x = pm.DiracDelta.dist(0.0)
y = x + sharedvar
draws = pm.draw(y, draws=5, mode=Mode('py'), updates={sharedvar: sharedvar + 1})
assert np.all(draws == np.arange(5))
```

## Next Steps


---

*Source: test_forward.py:109 | Complexity: Intermediate | Last updated: 2026-05-18*