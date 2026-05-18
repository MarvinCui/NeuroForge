# How To: Datatype

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datatype

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

### Step 1: Assign ehdr = self.header_class(...)

```python
ehdr = self.header_class()
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 2: Assign codes = value

```python
codes = self.header_class._data_type_codes
```

**Verification:**
```python
assert ehdr['bitpix'] == dt.itemsize * 8
```

### Step 3: Assign npt = value

```python
npt = codes.type[code]
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 4: Assign dt = value

```python
dt = codes.dtype[code]
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 5: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(npt)
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 6: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(code)
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 7: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(dt)
```

**Verification:**
```python
assert ehdr['datatype'] == code
```

### Step 8: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(code)
```


## Complete Example

```python
# Workflow
ehdr = self.header_class()
codes = self.header_class._data_type_codes
for code in codes.value_set():
    npt = codes.type[code]
    if npt is np.void:
        with pytest.raises(HeaderDataError):
            ehdr.set_data_dtype(code)
        continue
    dt = codes.dtype[code]
    ehdr.set_data_dtype(npt)
    assert ehdr['datatype'] == code
    assert ehdr['bitpix'] == dt.itemsize * 8
    ehdr.set_data_dtype(code)
    assert ehdr['datatype'] == code
    ehdr.set_data_dtype(dt)
    assert ehdr['datatype'] == code
```

## Next Steps


---

*Source: test_analyze.py:403 | Complexity: Advanced | Last updated: 2026-05-18*