# How To: General Init

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test general init

## Prerequisites

**Required Modules:**
- `logging`
- `numpy`
- `wrapstruct`
- `batteryrunners`
- `py3k`
- `volumeutils`
- `spatialimages`
- `unittest`
- `numpy.testing`
- `testing`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_equal(len(binblock), hdr.structarr.dtype.itemsize)
```

### Step 2: Assign binblock = value

```python
binblock = hdr.binaryblock
```

**Verification:**
```python
assert_equal(hdr.endianness, native_code)
```

### Step 3: Call assert_equal()

```python
assert_equal(len(binblock), hdr.structarr.dtype.itemsize)
```

**Verification:**
```python
assert_equal(hdr.endianness, swapped_code)
```

### Step 4: Call assert_equal()

```python
assert_equal(hdr.endianness, native_code)
```

### Step 5: Assign hdr = self.header_class(...)

```python
hdr = self.header_class(endianness='swapped')
```

### Step 6: Call assert_equal()

```python
assert_equal(hdr.endianness, swapped_code)
```

### Step 7: Assign hdr = self.header_class(...)

```python
hdr = self.header_class(check=False)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
binblock = hdr.binaryblock
assert_equal(len(binblock), hdr.structarr.dtype.itemsize)
assert_equal(hdr.endianness, native_code)
hdr = self.header_class(endianness='swapped')
assert_equal(hdr.endianness, swapped_code)
hdr = self.header_class(check=False)
```

## Next Steps


---

*Source: test_wrapstruct.py:110 | Complexity: Intermediate | Last updated: 2026-05-18*