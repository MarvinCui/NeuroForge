# How To: Find Data Skips Deterministics

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find data skips deterministics

## Prerequisites

**Required Modules:**
- `logging`
- `numpy`
- `pytest`
- `xarray`
- `pymc`
- `pymc.backends`
- `pymc.pytensorf`
- `pymc.step_methods`
- `pymc.step_methods.arraystep`
- `pymc.backends.mcbackend`
- `mcbackend`
- `mcbackend.npproto.utils`


## Step-by-Step Guide

### Step 1: Assign data = np.array(...)

```python
data = np.array([0, 1], dtype='float32')
```

**Verification:**
```python
assert 'c' in pmodel.named_vars
```

### Step 2: Assign dvars = find_data(...)

```python
dvars = find_data(pmodel)
```

**Verification:**
```python
assert len(dvars) == 1
```

### Step 3: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(ndarray_to_numpy(dvars[0].value), data)
```

**Verification:**
```python
assert dvars[0].name == 'a'
```

### Step 4: Assign a = pm.Data(...)

```python
a = pm.Data('a', data, dims='item')
```

**Verification:**
```python
assert dvars[0].dims == ['item']
```

### Step 5: Assign b = pm.Normal(...)

```python
b = pm.Normal('b')
```

**Verification:**
```python
assert not dvars[0].is_observed
```

### Step 6: Call pm.Deterministic()

```python
pm.Deterministic('c', a + b, dims='item')
```


## Complete Example

```python
# Workflow
data = np.array([0, 1], dtype='float32')
with pm.Model() as pmodel:
    a = pm.Data('a', data, dims='item')
    b = pm.Normal('b')
    pm.Deterministic('c', a + b, dims='item')
assert 'c' in pmodel.named_vars
dvars = find_data(pmodel)
assert len(dvars) == 1
assert dvars[0].name == 'a'
assert dvars[0].dims == ['item']
np.testing.assert_array_equal(ndarray_to_numpy(dvars[0].value), data)
assert not dvars[0].is_observed
```

## Next Steps


---

*Source: test_mcbackend.py:79 | Complexity: Intermediate | Last updated: 2026-05-18*