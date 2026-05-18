# How To: General Init

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test general init

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
assert len(binblock) == hdr.structarr.dtype.itemsize
```

### Step 2: Assign binblock = value

```python
binblock = hdr.binaryblock
```

**Verification:**
```python
assert hdr.endianness == native_code
```

### Step 3: Assign hdr = self.header_class(...)

```python
hdr = self.header_class(endianness='swapped')
```

**Verification:**
```python
assert hdr.endianness == swapped_code
```

### Step 4: Assign hdr = self.header_class(...)

```python
hdr = self.header_class(check=False)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
binblock = hdr.binaryblock
assert len(binblock) == hdr.structarr.dtype.itemsize
assert hdr.endianness == native_code
hdr = self.header_class(endianness='swapped')
assert hdr.endianness == swapped_code
hdr = self.header_class(check=False)
```

## Next Steps


---

*Source: test_wrapstruct.py:118 | Complexity: Intermediate | Last updated: 2026-05-18*