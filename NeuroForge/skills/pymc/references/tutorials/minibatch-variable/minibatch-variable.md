# How To: Minibatch Variable

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test minibatch variable

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pandas`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.sparse`
- `pytensor`
- `pytensor.compile`
- `pytensor.compile.builders`
- `pytensor.graph.basic`
- `pytensor.link.vm`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.data`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`
- `pymc.exceptions`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.vartypes`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign x = np.arange(...)

```python
x = np.arange(5)
```

**Verification:**
```python
assert isinstance(x_mb.owner.op, MinibatchOp)
```

### Step 2: Assign y = value

```python
y = x * 2
```

**Verification:**
```python
assert isinstance(y_mb.owner.op, MinibatchOp)
```

### Step 3: Assign unknown = Minibatch(...)

```python
x_mb, y_mb = Minibatch(x, y, batch_size=2)
```

**Verification:**
```python
assert isinstance(res, np.ndarray)
```

### Step 4: Assign res = extract_obs_data(...)

```python
res = extract_obs_data(x_mb)
```

**Verification:**
```python
assert isinstance(res, np.ndarray)
```

### Step 5: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(res, x)
```

### Step 6: Assign res = extract_obs_data(...)

```python
res = extract_obs_data(y_mb)
```

**Verification:**
```python
assert isinstance(res, np.ndarray)
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(res, y)
```


## Complete Example

```python
# Workflow
x = np.arange(5)
y = x * 2
x_mb, y_mb = Minibatch(x, y, batch_size=2)
assert isinstance(x_mb.owner.op, MinibatchOp)
assert isinstance(y_mb.owner.op, MinibatchOp)
res = extract_obs_data(x_mb)
assert isinstance(res, np.ndarray)
np.testing.assert_array_equal(res, x)
res = extract_obs_data(y_mb)
assert isinstance(res, np.ndarray)
np.testing.assert_array_equal(res, y)
```

## Next Steps


---

*Source: test_pytensorf.py:184 | Complexity: Intermediate | Last updated: 2026-05-18*