# How To: Mappingness

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test mappingness

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
assert_raises(ValueError, hdr.__setitem__, 'nonexistent key', 0.1)
```

### Step 2: Call assert_raises()

```python
assert_raises(ValueError, hdr.__setitem__, 'nonexistent key', 0.1)
```

**Verification:**
```python
assert_equal(keys, list(hdr))
```

### Step 3: Assign hdr_dt = value

```python
hdr_dt = hdr.structarr.dtype
```

**Verification:**
```python
assert_equal(len(vals), len(keys))
```

### Step 4: Assign keys = hdr.keys(...)

```python
keys = hdr.keys()
```

**Verification:**
```python
assert_equal(keys, list(hdr_dt.names))
```

### Step 5: Call assert_equal()

```python
assert_equal(keys, list(hdr))
```

**Verification:**
```python
assert_array_equal(hdr[key], val)
```

### Step 6: Assign vals = hdr.values(...)

```python
vals = hdr.values()
```

**Verification:**
```python
assert_equal(hdr.get('nonexistent key'), None)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(vals), len(keys))
```

**Verification:**
```python
assert_equal(hdr.get('nonexistent key', 'default'), 'default')
```

### Step 8: Call assert_equal()

```python
assert_equal(keys, list(hdr_dt.names))
```

**Verification:**
```python
assert_equal(hdr.get(keys[0]), vals[0])
```

### Step 9: Call assert_equal()

```python
assert_equal(hdr.get('nonexistent key'), None)
```

**Verification:**
```python
assert_equal(hdr.get(keys[0], 'default'), vals[0])
```

### Step 10: Call assert_equal()

```python
assert_equal(hdr.get('nonexistent key', 'default'), 'default')
```

### Step 11: Call assert_equal()

```python
assert_equal(hdr.get(keys[0]), vals[0])
```

### Step 12: Call assert_equal()

```python
assert_equal(hdr.get(keys[0], 'default'), vals[0])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(hdr[key], val)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
assert_raises(ValueError, hdr.__setitem__, 'nonexistent key', 0.1)
hdr_dt = hdr.structarr.dtype
keys = hdr.keys()
assert_equal(keys, list(hdr))
vals = hdr.values()
assert_equal(len(vals), len(keys))
assert_equal(keys, list(hdr_dt.names))
for key, val in hdr.items():
    assert_array_equal(hdr[key], val)
assert_equal(hdr.get('nonexistent key'), None)
assert_equal(hdr.get('nonexistent key', 'default'), 'default')
assert_equal(hdr.get(keys[0]), vals[0])
assert_equal(hdr.get(keys[0], 'default'), vals[0])
```

## Next Steps


---

*Source: test_wrapstruct.py:154 | Complexity: Advanced | Last updated: 2026-05-18*