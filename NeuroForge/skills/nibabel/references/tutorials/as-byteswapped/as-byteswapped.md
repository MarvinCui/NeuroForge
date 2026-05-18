# How To: As Byteswapped

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test as byteswapped

## Prerequisites

**Required Modules:**
- `logging`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `batteryrunners`
- `casting`
- `spatialimages`
- `volumeutils`
- `wrapstruct`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert hdr.endianness == native_code
```

### Step 2: Assign hdr2 = hdr.as_byteswapped(...)

```python
hdr2 = hdr.as_byteswapped(native_code)
```

**Verification:**
```python
assert not hdr is hdr2
```

### Step 3: Assign hdr_bs = hdr.as_byteswapped(...)

```python
hdr_bs = hdr.as_byteswapped(swapped_code)
```

**Verification:**
```python
assert hdr_bs.endianness == swapped_code
```

### Step 4: Assign hdr = DC(...)

```python
hdr = DC(hdr.binaryblock, check=False)
```

**Verification:**
```python
assert hdr.binaryblock != hdr_bs.binaryblock
```

### Step 5: Assign hdr2 = hdr.as_byteswapped(...)

```python
hdr2 = hdr.as_byteswapped(native_code)
```

### Step 6: Assign hdr_bs = hdr.as_byteswapped(...)

```python
hdr_bs = hdr.as_byteswapped(swapped_code)
```

### Step 7: Call DC()

```python
DC(hdr.binaryblock)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
assert hdr.endianness == native_code
hdr2 = hdr.as_byteswapped(native_code)
assert not hdr is hdr2
hdr_bs = hdr.as_byteswapped(swapped_code)
assert hdr_bs.endianness == swapped_code
assert hdr.binaryblock != hdr_bs.binaryblock

class DC(self.header_class):

    def check_fix(self, *args, **kwargs):
        raise Exception
with pytest.raises(Exception):
    DC(hdr.binaryblock)
hdr = DC(hdr.binaryblock, check=False)
hdr2 = hdr.as_byteswapped(native_code)
hdr_bs = hdr.as_byteswapped(swapped_code)
```

## Next Steps


---

*Source: test_wrapstruct.py:270 | Complexity: Intermediate | Last updated: 2026-05-18*