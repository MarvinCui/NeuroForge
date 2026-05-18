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
- `shutil`
- `tempfile`
- `glob`
- `numpy`
- `py3k`
- `netcdf`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign eg_sio1 = BytesIO(...)

```python
eg_sio1 = BytesIO()
```

### Step 2: Assign f1 = make_simple(...)

```python
f1 = make_simple(eg_sio1, 'w')
```

### Step 3: Assign str_val = eg_sio1.getvalue(...)

```python
str_val = eg_sio1.getvalue()
```

### Step 4: Call f1.close()

```python
f1.close()
```

### Step 5: Assign eg_sio2 = BytesIO(...)

```python
eg_sio2 = BytesIO(str_val)
```

### Step 6: Assign f2 = netcdf_file(...)

```python
f2 = netcdf_file(eg_sio2)
```

### Step 7: Call f2.close()

```python
f2.close()
```

### Step 8: Assign eg_sio3 = BytesIO(...)

```python
eg_sio3 = BytesIO(str_val)
```

### Step 9: yield (assert_raises, ValueError, netcdf_file, eg_sio3, 'r', True)

```python
yield (assert_raises, ValueError, netcdf_file, eg_sio3, 'r', True)
```

### Step 10: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO()
```

### Step 11: Assign f_64 = make_simple(...)

```python
f_64 = make_simple(eg_sio_64, 'w', version=2)
```

### Step 12: Assign str_val = eg_sio_64.getvalue(...)

```python
str_val = eg_sio_64.getvalue()
```

### Step 13: Call f_64.close()

```python
f_64.close()
```

### Step 14: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO(str_val)
```

### Step 15: Assign f_64 = netcdf_file(...)

```python
f_64 = netcdf_file(eg_sio_64)
```

### Step 16: yield (assert_equal, f_64.version_byte, 2)

```python
yield (assert_equal, f_64.version_byte, 2)
```

### Step 17: Assign eg_sio_64 = BytesIO(...)

```python
eg_sio_64 = BytesIO(str_val)
```

### Step 18: Assign f_64 = netcdf_file(...)

```python
f_64 = netcdf_file(eg_sio_64, version=2)
```

### Step 19: yield (assert_equal, f_64.version_byte, 2)

```python
yield (assert_equal, f_64.version_byte, 2)
```

### Step 20: yield testargs

```python
yield testargs
```

### Step 21: yield testargs

```python
yield testargs
```

### Step 22: yield testargs

```python
yield testargs
```


## Complete Example

```python
# Workflow
eg_sio1 = BytesIO()
f1 = make_simple(eg_sio1, 'w')
str_val = eg_sio1.getvalue()
f1.close()
eg_sio2 = BytesIO(str_val)
f2 = netcdf_file(eg_sio2)
for testargs in gen_for_simple(f2):
    yield testargs
f2.close()
eg_sio3 = BytesIO(str_val)
yield (assert_raises, ValueError, netcdf_file, eg_sio3, 'r', True)
eg_sio_64 = BytesIO()
f_64 = make_simple(eg_sio_64, 'w', version=2)
str_val = eg_sio_64.getvalue()
f_64.close()
eg_sio_64 = BytesIO(str_val)
f_64 = netcdf_file(eg_sio_64)
for testargs in gen_for_simple(f_64):
    yield testargs
yield (assert_equal, f_64.version_byte, 2)
eg_sio_64 = BytesIO(str_val)
f_64 = netcdf_file(eg_sio_64, version=2)
for testargs in gen_for_simple(f_64):
    yield testargs
yield (assert_equal, f_64.version_byte, 2)
```

## Next Steps


---

*Source: test_netcdf.py:84 | Complexity: Advanced | Last updated: 2026-05-18*