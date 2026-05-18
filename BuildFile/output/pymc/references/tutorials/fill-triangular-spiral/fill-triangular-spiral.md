# How To: Fill Triangular Spiral

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fill triangular spiral

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.pytensorf`
- `pymc.testing`
- `numpy`

**Setup Required:**
```python
# Fixtures: upper
```

## Step-by-Step Guide

### Step 1: Assign x_unconstrained = np.array(...)

```python
x_unconstrained = np.array([1, 2, 3, 4, 5, 6])
```

### Step 2: Assign transform = tr.CholeskyCorrTransform(...)

```python
transform = tr.CholeskyCorrTransform(n=3, upper=upper)
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(transform._fill_triangular_spiral(x_unconstrained, unit_diag=False).eval(), x_constrained)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(transform._inverse_fill_triangular_spiral(x_constrained, unit_diag=False).eval(), x_unconstrained)
```

### Step 5: Assign x_constrained = np.array(...)

```python
x_constrained = np.array([[1, 2, 3], [0, 5, 6], [0, 0, 4]])
```

### Step 6: Assign x_constrained = np.array(...)

```python
x_constrained = np.array([[4, 0, 0], [6, 5, 0], [3, 2, 1]])
```


## Complete Example

```python
# Setup
# Fixtures: upper

# Workflow
x_unconstrained = np.array([1, 2, 3, 4, 5, 6])
if upper:
    x_constrained = np.array([[1, 2, 3], [0, 5, 6], [0, 0, 4]])
else:
    x_constrained = np.array([[4, 0, 0], [6, 5, 0], [3, 2, 1]])
transform = tr.CholeskyCorrTransform(n=3, upper=upper)
np.testing.assert_allclose(transform._fill_triangular_spiral(x_unconstrained, unit_diag=False).eval(), x_constrained)
np.testing.assert_allclose(transform._inverse_fill_triangular_spiral(x_constrained, unit_diag=False).eval(), x_unconstrained)
```

## Next Steps


---

*Source: test_transform.py:697 | Complexity: Intermediate | Last updated: 2026-05-18*