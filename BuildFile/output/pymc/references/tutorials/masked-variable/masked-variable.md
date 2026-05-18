# How To: Masked Variable

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test masked variable

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

### Step 1: Assign data = np.random.normal(...)

```python
data = np.random.normal(size=(2, 3))
```

**Verification:**
```python
assert isinstance(z_at.owner.op, AdvancedIncSubtensor)
```

### Step 2: Assign data_pt = pt.as_tensor(...)

```python
data_pt = pt.as_tensor(data)
```

**Verification:**
```python
assert isinstance(res, np.ndarray)
```

### Step 3: Assign mask = np.random.binomial.astype(...)

```python
mask = np.random.binomial(1, 0.5, size=(2, 3)).astype(bool)
```

**Verification:**
```python
assert np.ma.allequal(res, data_m)
```

### Step 4: Assign data_m = np.ma.MaskedArray(...)

```python
data_m = np.ma.MaskedArray(data, mask)
```

### Step 5: Assign missing_values = value

```python
missing_values = data_pt.type()[mask]
```

### Step 6: Assign constant = pt.as_tensor(...)

```python
constant = pt.as_tensor(data_m.filled())
```

### Step 7: Assign z_at = pt.set_subtensor(...)

```python
z_at = pt.set_subtensor(constant[mask.nonzero()], missing_values)
```

**Verification:**
```python
assert isinstance(z_at.owner.op, AdvancedIncSubtensor)
```

### Step 8: Assign res = extract_obs_data(...)

```python
res = extract_obs_data(z_at)
```

**Verification:**
```python
assert isinstance(res, np.ndarray)
```


## Complete Example

```python
# Workflow
data = np.random.normal(size=(2, 3))
data_pt = pt.as_tensor(data)
mask = np.random.binomial(1, 0.5, size=(2, 3)).astype(bool)
data_m = np.ma.MaskedArray(data, mask)
missing_values = data_pt.type()[mask]
constant = pt.as_tensor(data_m.filled())
z_at = pt.set_subtensor(constant[mask.nonzero()], missing_values)
assert isinstance(z_at.owner.op, AdvancedIncSubtensor)
res = extract_obs_data(z_at)
assert isinstance(res, np.ndarray)
assert np.ma.allequal(res, data_m)
```

## Next Steps


---

*Source: test_pytensorf.py:158 | Complexity: Advanced | Last updated: 2026-05-18*