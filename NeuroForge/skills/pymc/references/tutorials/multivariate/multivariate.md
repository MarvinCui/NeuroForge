# How To: Multivariate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivariate

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

### Step 1: Assign mln_draws = pm.draw(...)

```python
mln_draws = pm.draw(mln, draws=1)
```

**Verification:**
```python
assert mln_draws.shape == (4,)
```

### Step 2: Assign unknown = pm.draw(...)

```python
mln_draws, = pm.draw([mln], draws=1)
```

**Verification:**
```python
assert mln_draws.shape == (4,)
```

### Step 3: Assign mln_draws = pm.draw(...)

```python
mln_draws = pm.draw(mln, draws=10)
```

**Verification:**
```python
assert mln_draws.shape == (10, 4)
```

### Step 4: Assign unknown = pm.draw(...)

```python
mln_draws, = pm.draw([mln], draws=10)
```

**Verification:**
```python
assert mln_draws.shape == (10, 4)
```

### Step 5: Assign mln = pm.Multinomial(...)

```python
mln = pm.Multinomial('mln', n=5, p=np.array([0.25, 0.25, 0.25, 0.25]))
```


## Complete Example

```python
# Workflow
with pm.Model():
    mln = pm.Multinomial('mln', n=5, p=np.array([0.25, 0.25, 0.25, 0.25]))
mln_draws = pm.draw(mln, draws=1)
assert mln_draws.shape == (4,)
mln_draws, = pm.draw([mln], draws=1)
assert mln_draws.shape == (4,)
mln_draws = pm.draw(mln, draws=10)
assert mln_draws.shape == (10, 4)
mln_draws, = pm.draw([mln], draws=10)
assert mln_draws.shape == (10, 4)
```

## Next Steps


---

*Source: test_forward.py:71 | Complexity: Intermediate | Last updated: 2026-05-18*