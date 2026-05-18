# How To: Mvstudentt Mu Convenience

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that mu is broadcasted to the length of scale and provided a default of zero

## Prerequisites

**Required Modules:**
- `functools`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pytensor.tensor.blockwise`
- `pytensor.tensor.linalg.decomposition.cholesky`
- `pytensor.tensor.linalg.inverse`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.math`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test that mu is broadcasted to the length of scale and provided a default of zero'

```python
'Test that mu is broadcasted to the length of scale and provided a default of zero'
```

### Step 2: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, scale=np.eye(3))
```

### Step 3: Assign mu = value

```python
mu = x.owner.inputs[3]
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mu.eval(), np.zeros((3,)))
```

### Step 5: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, mu=1, scale=np.eye(3))
```

### Step 6: Assign mu = value

```python
mu = x.owner.inputs[3]
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mu.eval(), np.ones((3,)))
```

### Step 8: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, mu=np.ones((1, 1)), scale=np.eye(3))
```

### Step 9: Assign mu = value

```python
mu = x.owner.inputs[3]
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mu.eval(), np.ones((1, 3)))
```

### Step 11: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, mu=np.ones((10, 1)), scale=np.eye(3))
```

### Step 12: Assign mu = value

```python
mu = x.owner.inputs[3]
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mu.eval(), np.ones((10, 3)))
```

### Step 14: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, mu=np.ones((10, 1, 1)), scale=np.full((2, 3, 3), np.eye(3)))
```

### Step 15: Assign mu = value

```python
mu = x.owner.inputs[3]
```

### Step 16: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mu.eval(), np.ones((10, 2, 3)))
```


## Complete Example

```python
# Workflow
'Test that mu is broadcasted to the length of scale and provided a default of zero'
x = pm.MvStudentT.dist(nu=4, scale=np.eye(3))
mu = x.owner.inputs[3]
np.testing.assert_allclose(mu.eval(), np.zeros((3,)))
x = pm.MvStudentT.dist(nu=4, mu=1, scale=np.eye(3))
mu = x.owner.inputs[3]
np.testing.assert_allclose(mu.eval(), np.ones((3,)))
x = pm.MvStudentT.dist(nu=4, mu=np.ones((1, 1)), scale=np.eye(3))
mu = x.owner.inputs[3]
np.testing.assert_allclose(mu.eval(), np.ones((1, 3)))
x = pm.MvStudentT.dist(nu=4, mu=np.ones((10, 1)), scale=np.eye(3))
mu = x.owner.inputs[3]
np.testing.assert_allclose(mu.eval(), np.ones((10, 3)))
x = pm.MvStudentT.dist(nu=4, mu=np.ones((10, 1, 1)), scale=np.full((2, 3, 3), np.eye(3)))
mu = x.owner.inputs[3]
np.testing.assert_allclose(mu.eval(), np.ones((10, 2, 3)))
```

## Next Steps


---

*Source: test_multivariate.py:2566 | Complexity: Advanced | Last updated: 2026-05-18*