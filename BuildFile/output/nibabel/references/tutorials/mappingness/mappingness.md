# How To: Mappingness

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mappingness

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
assert keys == list(hdr)
```

### Step 2: Assign hdr_dt = value

```python
hdr_dt = hdr.structarr.dtype
```

**Verification:**
```python
assert len(vals) == len(keys)
```

### Step 3: Assign keys = hdr.keys(...)

```python
keys = hdr.keys()
```

**Verification:**
```python
assert keys == list(hdr_dt.names)
```

### Step 4: Assign vals = hdr.values(...)

```python
vals = hdr.values()
```

**Verification:**
```python
assert_array_equal(hdr[key], val)
```

### Step 5: Assign falsyval = value

```python
falsyval = 0 if np.issubdtype(hdr_dt[0], np.number) else b''
```

**Verification:**
```python
assert hdr.get('nonexistent key') is None
```

### Step 6: Assign unknown = falsyval

```python
hdr[keys[0]] = falsyval
```

**Verification:**
```python
assert hdr.get('nonexistent key', 'default') == 'default'
```

### Step 7: Assign unknown = 0.1

```python
hdr['nonexistent key'] = 0.1
```

**Verification:**
```python
assert hdr.get(keys[0]) == vals[0]
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(hdr[key], val)
```

**Verification:**
```python
assert hdr.get(keys[0], 'default') == vals[0]
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
with pytest.raises(ValueError):
    hdr['nonexistent key'] = 0.1
hdr_dt = hdr.structarr.dtype
keys = hdr.keys()
assert keys == list(hdr)
vals = hdr.values()
assert len(vals) == len(keys)
assert keys == list(hdr_dt.names)
for key, val in hdr.items():
    assert_array_equal(hdr[key], val)
assert hdr.get('nonexistent key') is None
assert hdr.get('nonexistent key', 'default') == 'default'
assert hdr.get(keys[0]) == vals[0]
assert hdr.get(keys[0], 'default') == vals[0]
falsyval = 0 if np.issubdtype(hdr_dt[0], np.number) else b''
hdr[keys[0]] = falsyval
assert hdr[keys[0]] == falsyval
assert hdr.get(keys[0]) == falsyval
assert hdr.get(keys[0], -1) == falsyval
```

## Next Steps


---

*Source: test_wrapstruct.py:162 | Complexity: Advanced | Last updated: 2026-05-18*