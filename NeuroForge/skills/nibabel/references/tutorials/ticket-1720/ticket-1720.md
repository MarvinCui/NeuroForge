# How To: Ticket 1720

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ticket 1720

## Prerequisites

**Required Modules:**
- `os`
- `os.path`
- `io`
- `glob`
- `contextlib`
- `numpy`
- `pytest`
- `netcdf`


## Step-by-Step Guide

### Step 1: Assign io = BytesIO(...)

```python
io = BytesIO()
```

**Verification:**
```python
assert f.history == b'Created for a test'
```

### Step 2: Assign items = value

```python
items = [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9]
```

**Verification:**
```python
assert float_var.units == b'metres'
```

### Step 3: Assign io = BytesIO(...)

```python
io = BytesIO(contents)
```

**Verification:**
```python
assert float_var.shape == (10,)
```

### Step 4: Assign f.history = 'Created for a test'

```python
f.history = 'Created for a test'
```

**Verification:**
```python
assert np.allclose(float_var[:], items)
```

### Step 5: Call f.createDimension()

```python
f.createDimension('float_var', 10)
```

### Step 6: Assign float_var = f.createVariable(...)

```python
float_var = f.createVariable('float_var', 'f', ('float_var',))
```

### Step 7: Assign unknown = items

```python
float_var[:] = items
```

### Step 8: Assign float_var.units = 'metres'

```python
float_var.units = 'metres'
```

### Step 9: Call f.flush()

```python
f.flush()
```

### Step 10: Assign contents = io.getvalue(...)

```python
contents = io.getvalue()
```

**Verification:**
```python
assert f.history == b'Created for a test'
```

### Step 11: Assign float_var = value

```python
float_var = f.variables['float_var']
```

**Verification:**
```python
assert float_var.units == b'metres'
```


## Complete Example

```python
# Workflow
io = BytesIO()
items = [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9]
with netcdf_file(io, 'w') as f:
    f.history = 'Created for a test'
    f.createDimension('float_var', 10)
    float_var = f.createVariable('float_var', 'f', ('float_var',))
    float_var[:] = items
    float_var.units = 'metres'
    f.flush()
    contents = io.getvalue()
io = BytesIO(contents)
with netcdf_file(io, 'r') as f:
    assert f.history == b'Created for a test'
    float_var = f.variables['float_var']
    assert float_var.units == b'metres'
    assert float_var.shape == (10,)
    assert np.allclose(float_var[:], items)
```

## Next Steps


---

*Source: test_netcdf.py:160 | Complexity: Advanced | Last updated: 2026-05-18*