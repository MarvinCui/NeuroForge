# How To: Get Variables And Point Fn

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get variables and point fn

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

### Step 1: Assign ip = simple_model.initial_point(...)

```python
ip = simple_model.initial_point()
```

**Verification:**
```python
assert isinstance(variables, list)
```

### Step 2: Assign unknown = get_variables_and_point_fn(...)

```python
variables, point_fn = get_variables_and_point_fn(simple_model, ip)
```

**Verification:**
```python
assert callable(point_fn)
```

### Step 3: Assign vdict = value

```python
vdict = {v.name: v for v in variables}
```

**Verification:**
```python
assert set(vdict) == {'integer', 'scalar', 'vector', 'vector_interval__', 'matrix'}
```

### Step 4: Assign point = point_fn(...)

```python
point = point_fn(ip)
```

**Verification:**
```python
assert len(point) == len(variables)
```


## Complete Example

```python
# Setup
# Fixtures: simple_model

# Workflow
ip = simple_model.initial_point()
variables, point_fn = get_variables_and_point_fn(simple_model, ip)
assert isinstance(variables, list)
assert callable(point_fn)
vdict = {v.name: v for v in variables}
assert set(vdict) == {'integer', 'scalar', 'vector', 'vector_interval__', 'matrix'}
point = point_fn(ip)
assert len(point) == len(variables)
for v, p in zip(variables, point):
    assert str(p.dtype) == v.dtype
```

## Next Steps


---

*Source: test_mcbackend.py:94 | Complexity: Intermediate | Last updated: 2026-05-18*