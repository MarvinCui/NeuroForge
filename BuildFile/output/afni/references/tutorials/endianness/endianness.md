# How To: Endianness

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test endianness

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `numpy`
- `py3k`
- `volumeutils`
- `ecat`
- `unittest`
- `nose.tools`
- `numpy.testing`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign native_hdr = self.header_class(...)

```python
native_hdr = self.header_class()
```

**Verification:**
```python
assert_true(native_hdr.endianness == native_code)
```

### Step 2: Call assert_true()

```python
assert_true(native_hdr.endianness == native_code)
```

**Verification:**
```python
assert_true(swapped_hdr.endianness == swapped_code)
```

### Step 3: Assign swapped_hdr = self.header_class(...)

```python
swapped_hdr = self.header_class(endianness=swapped_code)
```

**Verification:**
```python
assert_true(file_hdr.endianness == '>')
```

### Step 4: Call assert_true()

```python
assert_true(swapped_hdr.endianness == swapped_code)
```

### Step 5: Assign fid = open(...)

```python
fid = open(ecat_file, 'rb')
```

### Step 6: Assign file_hdr = native_hdr.from_fileobj(...)

```python
file_hdr = native_hdr.from_fileobj(fid)
```

### Step 7: Call fid.close()

```python
fid.close()
```

### Step 8: Call assert_true()

```python
assert_true(file_hdr.endianness == '>')
```


## Complete Example

```python
# Workflow
native_hdr = self.header_class()
assert_true(native_hdr.endianness == native_code)
swapped_hdr = self.header_class(endianness=swapped_code)
assert_true(swapped_hdr.endianness == swapped_code)
fid = open(ecat_file, 'rb')
file_hdr = native_hdr.from_fileobj(fid)
fid.close()
assert_true(file_hdr.endianness == '>')
```

## Next Steps


---

*Source: test_ecat.py:76 | Complexity: Advanced | Last updated: 2026-05-18*