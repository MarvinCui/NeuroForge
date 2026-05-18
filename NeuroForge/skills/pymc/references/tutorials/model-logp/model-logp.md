# How To: Model Logp

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test model logp

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pickle`
- `threading`
- `traceback`
- `warnings`
- `unittest.mock`
- `arviz`
- `cloudpickle`
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pytensor`
- `pytensor.sparse`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.sparse`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.link.numba`
- `pytensor.raise_op`
- `pytensor.tensor.random.op`
- `pytensor.tensor.variable`
- `pymc`
- `pymc`
- `pymc.blocking`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.variational.minibatch_rv`
- `tests.models`

**Setup Required:**
```python
# Fixtures: jacobian
```

## Step-by-Step Guide

### Step 1: Assign test_vals = np.array(...)

```python
test_vals = np.array([0.0, 1.0])
```

**Verification:**
```python
assert np.all(np.isclose(x_logp, expected_x_logp))
```

### Step 2: Assign expected_x_logp = st.norm.logpdf(...)

```python
expected_x_logp = st.norm().logpdf(test_vals)
```

**Verification:**
```python
assert np.all(np.isclose(y_logp, expected_y_logp))
```

### Step 3: Assign expected_y_logp = expected_x_logp.copy(...)

```python
expected_y_logp = expected_x_logp.copy()
```

**Verification:**
```python
assert np.all(np.isclose(x_logp2, expected_x_logp))
```

### Step 4: Assign test_val_dict = value

```python
test_val_dict = {'x': test_vals, 'y_log__': test_vals}
```

**Verification:**
```python
assert np.all(np.isclose(y_logp2, expected_y_logp))
```

### Step 5: Assign unknown = m.compile_logp(...)

```python
x_logp, y_logp = m.compile_logp(sum=False, jacobian=jacobian)(test_val_dict)
```

**Verification:**
```python
assert np.isclose(logp_sum, expected_x_logp.sum() + expected_y_logp.sum())
```

### Step 6: Assign x_logp2 = m.compile_logp(...)

```python
x_logp2 = m.compile_logp(vars=[x], sum=False, jacobian=jacobian)(test_val_dict)
```

**Verification:**
```python
assert np.all(np.isclose(x_logp2, expected_x_logp))
```

### Step 7: Assign y_logp2 = m.compile_logp(...)

```python
y_logp2 = m.compile_logp(vars=[y], sum=False, jacobian=jacobian)(test_val_dict)
```

**Verification:**
```python
assert np.all(np.isclose(y_logp2, expected_y_logp))
```

### Step 8: Assign logp_sum = m.compile_logp(...)

```python
logp_sum = m.compile_logp(sum=True, jacobian=jacobian)(test_val_dict)
```

**Verification:**
```python
assert np.isclose(logp_sum, expected_x_logp.sum() + expected_y_logp.sum())
```

### Step 9: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, 1, size=2)
```

### Step 10: Assign y = pm.LogNormal(...)

```python
y = pm.LogNormal('y', 0, 1, size=2)
```


## Complete Example

```python
# Setup
# Fixtures: jacobian

# Workflow
with pm.Model() as m:
    x = pm.Normal('x', 0, 1, size=2)
    y = pm.LogNormal('y', 0, 1, size=2)
test_vals = np.array([0.0, 1.0])
expected_x_logp = st.norm().logpdf(test_vals)
expected_y_logp = expected_x_logp.copy()
if not jacobian:
    expected_y_logp -= np.array([0.0, 1.0])
test_val_dict = {'x': test_vals, 'y_log__': test_vals}
x_logp, y_logp = m.compile_logp(sum=False, jacobian=jacobian)(test_val_dict)
assert np.all(np.isclose(x_logp, expected_x_logp))
assert np.all(np.isclose(y_logp, expected_y_logp))
x_logp2 = m.compile_logp(vars=[x], sum=False, jacobian=jacobian)(test_val_dict)
assert np.all(np.isclose(x_logp2, expected_x_logp))
y_logp2 = m.compile_logp(vars=[y], sum=False, jacobian=jacobian)(test_val_dict)
assert np.all(np.isclose(y_logp2, expected_y_logp))
logp_sum = m.compile_logp(sum=True, jacobian=jacobian)(test_val_dict)
assert np.isclose(logp_sum, expected_x_logp.sum() + expected_y_logp.sum())
```

## Next Steps


---

*Source: test_core.py:1056 | Complexity: Advanced | Last updated: 2026-05-18*