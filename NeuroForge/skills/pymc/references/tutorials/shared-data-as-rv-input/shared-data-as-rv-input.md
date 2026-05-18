# How To: Shared Data As Rv Input

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Allow pm.Data to be used as input for other RVs.
See https://github.com/pymc-devs/pymc/issues/3842

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: '\n        Allow pm.Data to be used as input for other RVs.\n        See https://github.com/pymc-devs/pymc/issues/3842\n        '

```python
'\n        Allow pm.Data to be used as input for other RVs.\n        See https://github.com/pymc-devs/pymc/issues/3842\n        '
```

**Verification:**
```python
assert y.eval().shape == (2, 3)
```

### Step 2: Assign samples = value

```python
samples = idata.posterior['y']
```

**Verification:**
```python
assert samples.shape == (1, 550, 2, 3)
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.array([1.0, 2.0, 3.0]), x.get_value(), atol=0.1)
```

**Verification:**
```python
assert y.eval().shape == (2, 3)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.array([1.0, 2.0, 3.0]), samples.mean(('chain', 'draw', 'y_dim_0')), atol=0.1)
```

**Verification:**
```python
assert samples.shape == (1, 620, 2, 3)
```

### Step 5: Assign samples = value

```python
samples = idata.posterior['y']
```

**Verification:**
```python
assert samples.shape == (1, 620, 2, 3)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.array([2.0, 4.0, 6.0]), x.get_value(), atol=0.1)
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.array([2.0, 4.0, 6.0]), samples.mean(('chain', 'draw', 'y_dim_0')), atol=0.1)
```

### Step 8: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0])
```

### Step 9: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', mu=x, size=(2, 3))
```

**Verification:**
```python
assert y.eval().shape == (2, 3)
```

### Step 10: Assign idata = pm.sample(...)

```python
idata = pm.sample(chains=1, tune=500, draws=550, return_inferencedata=True, compute_convergence_checks=False)
```

### Step 11: Call pm.set_data()

```python
pm.set_data({'x': np.array([2.0, 4.0, 6.0])})
```

**Verification:**
```python
assert y.eval().shape == (2, 3)
```

### Step 12: Assign idata = pm.sample(...)

```python
idata = pm.sample(chains=1, tune=500, draws=620, return_inferencedata=True, compute_convergence_checks=False)
```


## Complete Example

```python
# Workflow
'\n        Allow pm.Data to be used as input for other RVs.\n        See https://github.com/pymc-devs/pymc/issues/3842\n        '
with pm.Model() as m:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Normal('y', mu=x, size=(2, 3))
    assert y.eval().shape == (2, 3)
    idata = pm.sample(chains=1, tune=500, draws=550, return_inferencedata=True, compute_convergence_checks=False)
samples = idata.posterior['y']
assert samples.shape == (1, 550, 2, 3)
np.testing.assert_allclose(np.array([1.0, 2.0, 3.0]), x.get_value(), atol=0.1)
np.testing.assert_allclose(np.array([1.0, 2.0, 3.0]), samples.mean(('chain', 'draw', 'y_dim_0')), atol=0.1)
with m:
    pm.set_data({'x': np.array([2.0, 4.0, 6.0])})
    assert y.eval().shape == (2, 3)
    idata = pm.sample(chains=1, tune=500, draws=620, return_inferencedata=True, compute_convergence_checks=False)
samples = idata.posterior['y']
assert samples.shape == (1, 620, 2, 3)
np.testing.assert_allclose(np.array([2.0, 4.0, 6.0]), x.get_value(), atol=0.1)
np.testing.assert_allclose(np.array([2.0, 4.0, 6.0]), samples.mean(('chain', 'draw', 'y_dim_0')), atol=0.1)
```

## Next Steps


---

*Source: test_data.py:184 | Complexity: Advanced | Last updated: 2026-05-18*