# How To: Flush Rewind

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test flush rewind

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

### Step 1: Assign stream = BytesIO(...)

```python
stream = BytesIO()
```

**Verification:**
```python
assert len_single == len_double
```

### Step 2: Assign x = f.createDimension(...)

```python
x = f.createDimension('x', 4)
```

### Step 3: Assign v = f.createVariable(...)

```python
v = f.createVariable('v', 'i2', ['x'])
```

### Step 4: Assign unknown = 1

```python
v[:] = 1
```

### Step 5: Call f.flush()

```python
f.flush()
```

### Step 6: Assign len_single = len(...)

```python
len_single = len(stream.getvalue())
```

### Step 7: Call f.flush()

```python
f.flush()
```

### Step 8: Assign len_double = len(...)

```python
len_double = len(stream.getvalue())
```


## Complete Example

```python
# Workflow
stream = BytesIO()
with make_simple(stream, mode='w') as f:
    x = f.createDimension('x', 4)
    v = f.createVariable('v', 'i2', ['x'])
    v[:] = 1
    f.flush()
    len_single = len(stream.getvalue())
    f.flush()
    len_double = len(stream.getvalue())
assert len_single == len_double
```

## Next Steps


---

*Source: test_netcdf.py:135 | Complexity: Advanced | Last updated: 2026-05-18*