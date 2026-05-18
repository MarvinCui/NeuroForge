# How To: As Byteswapped

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test as byteswapped

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
assert_equal(hdr.endianness, native_code)
```

### Step 2: Call assert_equal()

```python
assert_equal(hdr.endianness, native_code)
```

**Verification:**
```python
assert_false(hdr is hdr2)
```

### Step 3: Assign hdr2 = hdr.as_byteswapped(...)

```python
hdr2 = hdr.as_byteswapped(native_code)
```

**Verification:**
```python
assert_equal(hdr_bs.endianness, swapped_code)
```

### Step 4: Call assert_false()

```python
assert_false(hdr is hdr2)
```

**Verification:**
```python
assert_not_equal(hdr.binaryblock, hdr_bs.binaryblock)
```

### Step 5: Assign hdr_bs = hdr.as_byteswapped(...)

```python
hdr_bs = hdr.as_byteswapped(swapped_code)
```

**Verification:**
```python
assert_raises(Exception, DC, hdr.binaryblock)
```

### Step 6: Call assert_equal()

```python
assert_equal(hdr_bs.endianness, swapped_code)
```

### Step 7: Call assert_not_equal()

```python
assert_not_equal(hdr.binaryblock, hdr_bs.binaryblock)
```

### Step 8: Call assert_raises()

```python
assert_raises(Exception, DC, hdr.binaryblock)
```

### Step 9: Assign hdr = DC(...)

```python
hdr = DC(hdr.binaryblock, check=False)
```

### Step 10: Assign hdr2 = hdr.as_byteswapped(...)

```python
hdr2 = hdr.as_byteswapped(native_code)
```

### Step 11: Assign hdr_bs = hdr.as_byteswapped(...)

```python
hdr_bs = hdr.as_byteswapped(swapped_code)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
assert_equal(hdr.endianness, native_code)
hdr2 = hdr.as_byteswapped(native_code)
assert_false(hdr is hdr2)
hdr_bs = hdr.as_byteswapped(swapped_code)
assert_equal(hdr_bs.endianness, swapped_code)
assert_not_equal(hdr.binaryblock, hdr_bs.binaryblock)

class DC(self.header_class):

    def check_fix(self, *args, **kwargs):
        raise Exception
assert_raises(Exception, DC, hdr.binaryblock)
hdr = DC(hdr.binaryblock, check=False)
hdr2 = hdr.as_byteswapped(native_code)
hdr_bs = hdr.as_byteswapped(swapped_code)
```

## Next Steps


---

*Source: test_wrapstruct.py:279 | Complexity: Advanced | Last updated: 2026-05-18*