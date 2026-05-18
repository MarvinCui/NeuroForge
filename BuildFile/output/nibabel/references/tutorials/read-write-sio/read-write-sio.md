# How To: Read Write Sio

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read write sio

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

### Step 1: Assign eg_sio1 = BytesIO(...)

```python
eg_sio1 = BytesIO()
```

**Verification:**
```python
assert_simple_truths(f2)
```

### Step 2: Assign eg_sio2 = BytesIO(...)

```python
eg_sio2 = BytesIO(str_val)
```

**Verification:**
```python
assert_simple_truths(f_64)
```

### Step 3: Assign eg_sio3 = BytesIO(...)

```python
eg_sio3 = BytesIO(str_val)
```

**Verification:**
```python
assert f_64.version_byte == 2
```

### Step 4: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO()
```

**Verification:**
```python
assert_simple_truths(f_64)
```

### Step 5: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO(str_val)
```

**Verification:**
```python
assert f_64.version_byte == 2
```

### Step 6: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO(str_val)
```

### Step 7: Assign str_val = eg_sio1.getvalue(...)

```python
str_val = eg_sio1.getvalue()
```

### Step 8: Call assert_simple_truths()

```python
assert_simple_truths(f2)
```

### Step 9: Call netcdf_file()

```python
netcdf_file(eg_sio3, 'r', True)
```

### Step 10: Assign str_val = eg_sio_64.getvalue(...)

```python
str_val = eg_sio_64.getvalue()
```

### Step 11: Call assert_simple_truths()

```python
assert_simple_truths(f_64)
```

**Verification:**
```python
assert f_64.version_byte == 2
```

### Step 12: Call assert_simple_truths()

```python
assert_simple_truths(f_64)
```

**Verification:**
```python
assert f_64.version_byte == 2
```


## Complete Example

```python
# Workflow
eg_sio1 = BytesIO()
with make_simple(eg_sio1, 'w') as f1:
    str_val = eg_sio1.getvalue()
eg_sio2 = BytesIO(str_val)
with netcdf_file(eg_sio2) as f2:
    assert_simple_truths(f2)
eg_sio3 = BytesIO(str_val)
with pytest.raises(ValueError):
    netcdf_file(eg_sio3, 'r', True)
eg_sio_64 = BytesIO()
with make_simple(eg_sio_64, 'w', version=2) as f_64:
    str_val = eg_sio_64.getvalue()
eg_sio_64 = BytesIO(str_val)
with netcdf_file(eg_sio_64) as f_64:
    assert_simple_truths(f_64)
    assert f_64.version_byte == 2
eg_sio_64 = BytesIO(str_val)
with netcdf_file(eg_sio_64, version=2) as f_64:
    assert_simple_truths(f_64)
    assert f_64.version_byte == 2
```

## Next Steps


---

*Source: test_netcdf.py:71 | Complexity: Advanced | Last updated: 2026-05-18*