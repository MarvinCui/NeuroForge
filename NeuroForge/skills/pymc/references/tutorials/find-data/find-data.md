# How To: Find Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find data

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: simple_model
```

## Step-by-Step Guide

### Step 1: Assign dvars = find_data(...)

```python
dvars = find_data(simple_model)
```

**Verification:**
```python
assert set(dvardict) == {'seconds', 'obs'}
```

### Step 2: Assign dvardict = value

```python
dvardict = {d.name: d for d in dvars}
```

**Verification:**
```python
assert isinstance(secs, mcb.DataVariable)
```

### Step 3: Assign secs = value

```python
secs = dvardict['seconds']
```

**Verification:**
```python
assert secs.dims == ['time']
```

### Step 4: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(ndarray_to_numpy(secs.value), simple_model['seconds'].get_value())
```

**Verification:**
```python
assert not secs.is_observed
```

### Step 5: Assign obs = value

```python
obs = dvardict['obs']
```

**Verification:**
```python
assert isinstance(obs, mcb.DataVariable)
```

### Step 6: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(ndarray_to_numpy(obs.value), simple_model['obs'].get_value())
```

**Verification:**
```python
assert obs.dims == ['condition', 'time']
```


## Complete Example

```python
# Setup
# Fixtures: simple_model

# Workflow
dvars = find_data(simple_model)
dvardict = {d.name: d for d in dvars}
assert set(dvardict) == {'seconds', 'obs'}
secs = dvardict['seconds']
assert isinstance(secs, mcb.DataVariable)
assert secs.dims == ['time']
assert not secs.is_observed
np.testing.assert_array_equal(ndarray_to_numpy(secs.value), simple_model['seconds'].get_value())
obs = dvardict['obs']
assert isinstance(obs, mcb.DataVariable)
assert obs.dims == ['condition', 'time']
assert obs.is_observed
np.testing.assert_array_equal(ndarray_to_numpy(obs.value), simple_model['obs'].get_value())
```

## Next Steps


---

*Source: test_mcbackend.py:61 | Complexity: Intermediate | Last updated: 2026-05-18*