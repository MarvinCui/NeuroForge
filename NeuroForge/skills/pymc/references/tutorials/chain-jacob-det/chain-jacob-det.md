# How To: Chain Jacob Det

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test chain jacob det

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign chain_tranf = tr.Chain(...)

```python
chain_tranf = tr.Chain([tr.logodds, tr.ordered])
```

**Verification:**
```python
assert_allclose(computed_ljd(floatX(np.array(y_val))), expected, rtol=1e-12, atol=1e-12)
```

### Step 2: Call check_jacobian_det()

```python
check_jacobian_det(chain_tranf, Vector(R, 4), pt.vector, floatX(np.zeros(4)), elemwise=False, tol=0.0001)
```

### Step 3: Assign test_points = value

```python
test_points = [([0, 0, 0, 0], -8.363848461389765), ([2.1, 2.1, 2.1, 2.1], -51.32812812107032), ([-1.0, 0.5, 1.0, -0.5], -9.561856735240324), ([0.01, -0.01, 1.0, 2.1], -15.573681776928918)]
```

### Step 4: Assign y_var = pt.vector(...)

```python
y_var = pt.vector('y')
```

### Step 5: Assign computed_ljd = function(...)

```python
computed_ljd = function([y_var], pt.as_tensor_variable(chain_tranf.log_jac_det(y_var)), on_unused_input='ignore')
```

### Step 6: Call assert_allclose()

```python
assert_allclose(computed_ljd(floatX(np.array(y_val))), expected, rtol=1e-12, atol=1e-12)
```


## Complete Example

```python
# Workflow
chain_tranf = tr.Chain([tr.logodds, tr.ordered])
check_jacobian_det(chain_tranf, Vector(R, 4), pt.vector, floatX(np.zeros(4)), elemwise=False, tol=0.0001)
if config.floatX == 'float64':
    test_points = [([0, 0, 0, 0], -8.363848461389765), ([2.1, 2.1, 2.1, 2.1], -51.32812812107032), ([-1.0, 0.5, 1.0, -0.5], -9.561856735240324), ([0.01, -0.01, 1.0, 2.1], -15.573681776928918)]
    y_var = pt.vector('y')
    computed_ljd = function([y_var], pt.as_tensor_variable(chain_tranf.log_jac_det(y_var)), on_unused_input='ignore')
    for y_val, expected in test_points:
        assert_allclose(computed_ljd(floatX(np.array(y_val))), expected, rtol=1e-12, atol=1e-12)
```

## Next Steps


---

*Source: test_transform.py:302 | Complexity: Intermediate | Last updated: 2026-05-18*