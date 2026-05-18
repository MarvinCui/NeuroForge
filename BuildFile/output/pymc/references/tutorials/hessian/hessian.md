# How To: Hessian

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hessian

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.tensor.random.basic`
- `scipy`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.dist_math`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign x = np.linspace(...)

```python
x = np.linspace(0, 1, 100)
```

### Step 2: Assign y = value

```python
y = x * x
```

### Step 3: Assign spline = SplineWrapper(...)

```python
spline = SplineWrapper(interpolate.InterpolatedUnivariateSpline(x, y, k=1))
```

### Step 4: Assign x_var = pt.dscalar(...)

```python
x_var = pt.dscalar('x')
```

### Step 5: Assign unknown = pt.grad(...)

```python
g_x, = pt.grad(spline(x_var), [x_var])
```

### Step 6: Call pt.grad()

```python
pt.grad(g_x, [x_var])
```


## Complete Example

```python
# Workflow
x = np.linspace(0, 1, 100)
y = x * x
spline = SplineWrapper(interpolate.InterpolatedUnivariateSpline(x, y, k=1))
x_var = pt.dscalar('x')
g_x, = pt.grad(spline(x_var), [x_var])
with pytest.raises(NotImplementedError):
    pt.grad(g_x, [x_var])
```

## Next Steps


---

*Source: test_dist_math.py:128 | Complexity: Intermediate | Last updated: 2026-05-18*