# How To: Log Jac Det

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test log jac det

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

### Step 1: Assign transform = tr.CholeskyCorrTransform(...)

```python
transform = tr.CholeskyCorrTransform(n=3, upper=False)
```

### Step 2: Assign unknown = self._get_test_values(...)

```python
x_unconstrained, _x_constrained = self._get_test_values()
```

### Step 3: Assign computed_log_jac_det = transform.log_jac_det.eval(...)

```python
computed_log_jac_det = transform.log_jac_det(x_unconstrained).eval()
```

### Step 4: Assign x = pt.tensor(...)

```python
x = pt.tensor('x', shape=(3,))
```

### Step 5: Assign lower_tri_vec = unknown.ravel(...)

```python
lower_tri_vec = transform.backward(x)[pt.tril_indices(x.shape[0], k=-1)].ravel()
```

### Step 6: Assign jac = pt.jacobian(...)

```python
jac = pt.jacobian(lower_tri_vec, x, vectorize=True)
```

### Step 7: Assign unknown = pt.linalg.slogdet(...)

```python
_, autodiff_log_jac_det = pt.linalg.slogdet(jac)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(autodiff_log_jac_det.eval({x: x_unconstrained}), computed_log_jac_det, atol=1e-06)
```


## Complete Example

```python
# Workflow
transform = tr.CholeskyCorrTransform(n=3, upper=False)
x_unconstrained, _x_constrained = self._get_test_values()
computed_log_jac_det = transform.log_jac_det(x_unconstrained).eval()
x = pt.tensor('x', shape=(3,))
lower_tri_vec = transform.backward(x)[pt.tril_indices(x.shape[0], k=-1)].ravel()
jac = pt.jacobian(lower_tri_vec, x, vectorize=True)
_, autodiff_log_jac_det = pt.linalg.slogdet(jac)
np.testing.assert_allclose(autodiff_log_jac_det.eval({x: x_unconstrained}), computed_log_jac_det, atol=1e-06)
```

## Next Steps


---

*Source: test_transform.py:759 | Complexity: Advanced | Last updated: 2026-05-18*