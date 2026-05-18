# How To: Datatype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datatype

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `logging`
- `pickle`
- `numpy`
- `py3k`
- `volumeutils`
- `spatialimages`
- `analyze`
- `nifti1`
- `loadsave`
- `casting`
- `numpy.testing`
- `testing`
- `test_wrapstruct`


## Step-by-Step Guide

### Step 1: Assign ehdr = self.header_class(...)

```python
ehdr = self.header_class()
```

**Verification:**
```python
assert_raises(HeaderDataError, ehdr.set_data_dtype, code)
```

### Step 2: Assign codes = value

```python
codes = self.header_class._data_type_codes
```

**Verification:**
```python
assert_true(ehdr['datatype'] == code)
```

### Step 3: Assign npt = value

```python
npt = codes.type[code]
```

**Verification:**
```python
assert_true(ehdr['bitpix'] == dt.itemsize * 8)
```

### Step 4: Assign dt = value

```python
dt = codes.dtype[code]
```

**Verification:**
```python
assert_true(ehdr['datatype'] == code)
```

### Step 5: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(npt)
```

**Verification:**
```python
assert_true(ehdr['datatype'] == code)
```

### Step 6: Call assert_true()

```python
assert_true(ehdr['datatype'] == code)
```

### Step 7: Call assert_true()

```python
assert_true(ehdr['bitpix'] == dt.itemsize * 8)
```

### Step 8: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(code)
```

### Step 9: Call assert_true()

```python
assert_true(ehdr['datatype'] == code)
```

### Step 10: Call ehdr.set_data_dtype()

```python
ehdr.set_data_dtype(dt)
```

### Step 11: Call assert_true()

```python
assert_true(ehdr['datatype'] == code)
```

### Step 12: Call assert_raises()

```python
assert_raises(HeaderDataError, ehdr.set_data_dtype, code)
```


## Complete Example

```python
# Workflow
ehdr = self.header_class()
codes = self.header_class._data_type_codes
for code in codes.value_set():
    npt = codes.type[code]
    if npt is np.void:
        assert_raises(HeaderDataError, ehdr.set_data_dtype, code)
        continue
    dt = codes.dtype[code]
    ehdr.set_data_dtype(npt)
    assert_true(ehdr['datatype'] == code)
    assert_true(ehdr['bitpix'] == dt.itemsize * 8)
    ehdr.set_data_dtype(code)
    assert_true(ehdr['datatype'] == code)
    ehdr.set_data_dtype(dt)
    assert_true(ehdr['datatype'] == code)
```

## Next Steps


---

*Source: test_analyze.py:312 | Complexity: Advanced | Last updated: 2026-05-18*