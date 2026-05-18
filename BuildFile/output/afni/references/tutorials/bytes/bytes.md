# How To: Bytes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test bytes

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

### Step 1: Assign hdr1 = self.header_class(...)

```python
hdr1 = self.header_class()
```

**Verification:**
```python
assert_equal(hdr1, hdr2)
```

### Step 2: Assign bb = value

```python
bb = hdr1.binaryblock
```

**Verification:**
```python
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
```

### Step 3: Assign hdr2 = self.header_class(...)

```python
hdr2 = self.header_class(hdr1.binaryblock)
```

**Verification:**
```python
assert_equal(hdr1, hdr2)
```

### Step 4: Call assert_equal()

```python
assert_equal(hdr1, hdr2)
```

**Verification:**
```python
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
```

### Step 5: Call assert_equal()

```python
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
```

**Verification:**
```python
assert_raises(WrapStructError, self.header_class, bb[:-1])
```

### Step 6: Call self._set_something_into_hdr()

```python
self._set_something_into_hdr(hdr1)
```

**Verification:**
```python
assert_raises(WrapStructError, self.header_class, bb + ZEROB)
```

### Step 7: Assign hdr2 = self.header_class(...)

```python
hdr2 = self.header_class(hdr1.binaryblock)
```

**Verification:**
```python
assert_raises(HeaderDataError, self.header_class, bb_bad)
```

### Step 8: Call assert_equal()

```python
assert_equal(hdr1, hdr2)
```

### Step 9: Call assert_equal()

```python
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
```

### Step 10: Call assert_raises()

```python
assert_raises(WrapStructError, self.header_class, bb[:-1])
```

### Step 11: Call assert_raises()

```python
assert_raises(WrapStructError, self.header_class, bb + ZEROB)
```

### Step 12: Assign bb_bad = value

```python
bb_bad = ZEROB * len(bb)
```

### Step 13: Call assert_raises()

```python
assert_raises(HeaderDataError, self.header_class, bb_bad)
```

### Step 14: Assign _ = self.header_class(...)

```python
_ = self.header_class(bb_bad, check=False)
```


## Complete Example

```python
# Workflow
hdr1 = self.header_class()
bb = hdr1.binaryblock
hdr2 = self.header_class(hdr1.binaryblock)
assert_equal(hdr1, hdr2)
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
self._set_something_into_hdr(hdr1)
hdr2 = self.header_class(hdr1.binaryblock)
assert_equal(hdr1, hdr2)
assert_equal(hdr1.binaryblock, hdr2.binaryblock)
assert_raises(WrapStructError, self.header_class, bb[:-1])
assert_raises(WrapStructError, self.header_class, bb + ZEROB)
bb_bad = ZEROB * len(bb)
assert_raises(HeaderDataError, self.header_class, bb_bad)
_ = self.header_class(bb_bad, check=False)
```

## Next Steps


---

*Source: test_wrapstruct.py:250 | Complexity: Advanced | Last updated: 2026-05-18*