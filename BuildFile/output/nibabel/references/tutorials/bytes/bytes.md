# How To: Bytes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bytes

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

### Step 1: Assign hdr1 = self.header_class(...)

```python
hdr1 = self.header_class()
```

**Verification:**
```python
assert hdr1 == hdr2
```

### Step 2: Assign bb = value

```python
bb = hdr1.binaryblock
```

**Verification:**
```python
assert hdr1.binaryblock == hdr2.binaryblock
```

### Step 3: Assign hdr2 = self.header_class(...)

```python
hdr2 = self.header_class(hdr1.binaryblock)
```

**Verification:**
```python
assert hdr1 == hdr2
```

### Step 4: Call self._set_something_into_hdr()

```python
self._set_something_into_hdr(hdr1)
```

**Verification:**
```python
assert hdr1.binaryblock == hdr2.binaryblock
```

### Step 5: Assign hdr2 = self.header_class(...)

```python
hdr2 = self.header_class(hdr1.binaryblock)
```

**Verification:**
```python
assert hdr1 == hdr2
```

### Step 6: Assign bb_bad = self.get_bad_bb(...)

```python
bb_bad = self.get_bad_bb()
```

### Step 7: Assign _ = self.header_class(...)

```python
_ = self.header_class(bb_bad, check=False)
```

### Step 8: Call self.header_class()

```python
self.header_class(bb[:-1])
```

### Step 9: Call self.header_class()

```python
self.header_class(bb + b'\x00')
```

### Step 10: Call self.header_class()

```python
self.header_class(bb_bad)
```


## Complete Example

```python
# Workflow
hdr1 = self.header_class()
bb = hdr1.binaryblock
hdr2 = self.header_class(hdr1.binaryblock)
assert hdr1 == hdr2
assert hdr1.binaryblock == hdr2.binaryblock
self._set_something_into_hdr(hdr1)
hdr2 = self.header_class(hdr1.binaryblock)
assert hdr1 == hdr2
assert hdr1.binaryblock == hdr2.binaryblock
with pytest.raises(WrapStructError):
    self.header_class(bb[:-1])
with pytest.raises(WrapStructError):
    self.header_class(bb + b'\x00')
bb_bad = self.get_bad_bb()
if bb_bad is None:
    return
with imageglobals.LoggingOutputSuppressor():
    with pytest.raises(HeaderDataError):
        self.header_class(bb_bad)
_ = self.header_class(bb_bad, check=False)
```

## Next Steps


---

*Source: test_wrapstruct.py:240 | Complexity: Advanced | Last updated: 2026-05-18*