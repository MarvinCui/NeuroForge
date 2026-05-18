# How To: Data Dtype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test data dtype

## Prerequisites

**Required Modules:**
- `itertools`
- `logging`
- `os`
- `pickle`
- `re`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `_compression`
- `analyze`
- `arraywriters`
- `casting`
- `nifti1`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign all_supported_types = value

```python
all_supported_types = ((2, np.uint8), (4, np.int16), (8, np.int32), (16, np.float32), (32, np.complex64), (64, np.float64), (128, np.dtype([('R', 'u1'), ('G', 'u1'), ('B', 'u1')])))
```

**Verification:**
```python
assert_dt_equal(hdr.get_data_dtype(), np_dtype)
```

### Step 2: Assign all_unsupported_types = value

```python
all_unsupported_types = (np.void, 'none', 'all', 0)
```

**Verification:**
```python
assert_set_dtype(code, npt)
```

### Step 3: Call assert_set_dtype()

```python
assert_set_dtype(float, np.float64)
```

**Verification:**
```python
assert_set_dtype(npt, npt)
```

### Step 4: Assign np_sys_int = value

```python
np_sys_int = np.dtype(int).type
```

**Verification:**
```python
assert_set_dtype(np.dtype(npt), npt)
```

### Step 5: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_set_dtype(npt, npt)
```

### Step 6: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_set_dtype(np.dtype(npt), npt)
```

### Step 7: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(dt_spec)
```

**Verification:**
```python
assert_set_dtype(np.dtype(npt).newbyteorder(), npt)
```

### Step 8: Call assert_dt_equal()

```python
assert_dt_equal(hdr.get_data_dtype(), np_dtype)
```

**Verification:**
```python
assert_set_dtype(np.dtype(npt).str, npt)
```

### Step 9: Call assert_set_dtype()

```python
assert_set_dtype(code, npt)
```

**Verification:**
```python
assert_set_dtype(np.dtype(npt).str[1:], npt)
```

### Step 10: Call assert_set_dtype()

```python
assert_set_dtype(npt, npt)
```

**Verification:**
```python
assert_set_dtype(float, np.float64)
```

### Step 11: Call assert_set_dtype()

```python
assert_set_dtype(np.dtype(npt), npt)
```

**Verification:**
```python
assert_set_dtype(int, np_sys_int)
```

### Step 12: Call assert_set_dtype()

```python
assert_set_dtype(npt, npt)
```

### Step 13: Call assert_set_dtype()

```python
assert_set_dtype(np.dtype(npt), npt)
```

### Step 14: Call assert_set_dtype()

```python
assert_set_dtype(np.dtype(npt).newbyteorder(), npt)
```

### Step 15: Call assert_set_dtype()

```python
assert_set_dtype(np.dtype(npt).str, npt)
```

### Step 16: Call assert_set_dtype()

```python
assert_set_dtype(np.dtype(npt).str[1:], npt)
```

### Step 17: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

### Step 18: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(int)
```

### Step 19: Call assert_set_dtype()

```python
assert_set_dtype(int, np_sys_int)
```

### Step 20: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(inp)
```


## Complete Example

```python
# Workflow
all_supported_types = ((2, np.uint8), (4, np.int16), (8, np.int32), (16, np.float32), (32, np.complex64), (64, np.float64), (128, np.dtype([('R', 'u1'), ('G', 'u1'), ('B', 'u1')])))
all_unsupported_types = (np.void, 'none', 'all', 0)

def assert_set_dtype(dt_spec, np_dtype):
    hdr = self.header_class()
    hdr.set_data_dtype(dt_spec)
    assert_dt_equal(hdr.get_data_dtype(), np_dtype)
for code, npt in all_supported_types:
    assert_set_dtype(code, npt)
    assert_set_dtype(npt, npt)
    assert_set_dtype(np.dtype(npt), npt)
for npt in self.supported_np_types:
    assert_set_dtype(npt, npt)
    assert_set_dtype(np.dtype(npt), npt)
    assert_set_dtype(np.dtype(npt).newbyteorder(), npt)
    assert_set_dtype(np.dtype(npt).str, npt)
    if np.dtype(npt).str[0] in '=|<>':
        assert_set_dtype(np.dtype(npt).str[1:], npt)
assert_set_dtype(float, np.float64)
np_sys_int = np.dtype(int).type
if issubclass(self.header_class, Nifti1Header):
    with pytest.raises(ValueError):
        hdr = self.header_class()
        hdr.set_data_dtype(int)
elif np_sys_int in self.supported_np_types:
    assert_set_dtype(int, np_sys_int)
hdr = self.header_class()
for inp in all_unsupported_types:
    with pytest.raises(HeaderDataError):
        hdr.set_data_dtype(inp)
```

## Next Steps


---

*Source: test_analyze.py:248 | Complexity: Advanced | Last updated: 2026-05-18*