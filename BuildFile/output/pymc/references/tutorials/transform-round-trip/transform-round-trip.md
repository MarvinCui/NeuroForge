# How To: Transform Round Trip

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transform round trip

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
x_unconstrained, x_constrained = self._get_test_values()
```

### Step 3: Assign constrained_reconstructed = transform.backward.eval(...)

```python
constrained_reconstructed = transform.backward(transform.forward(x_constrained)).eval()
```

### Step 4: Assign unconstrained_reconstructed = transform.forward.eval(...)

```python
unconstrained_reconstructed = transform.forward(transform.backward(x_unconstrained)).eval()
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_unconstrained, unconstrained_reconstructed, atol=1e-06)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_constrained, constrained_reconstructed, atol=1e-06)
```


## Complete Example

```python
# Workflow
transform = tr.CholeskyCorrTransform(n=3, upper=False)
x_unconstrained, x_constrained = self._get_test_values()
constrained_reconstructed = transform.backward(transform.forward(x_constrained)).eval()
unconstrained_reconstructed = transform.forward(transform.backward(x_unconstrained)).eval()
np.testing.assert_allclose(x_unconstrained, unconstrained_reconstructed, atol=1e-06)
np.testing.assert_allclose(x_constrained, constrained_reconstructed, atol=1e-06)
```

## Next Steps


---

*Source: test_transform.py:749 | Complexity: Intermediate | Last updated: 2026-05-18*