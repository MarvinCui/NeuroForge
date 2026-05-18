# How To: Write Mgh

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test write mgh

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `numpy`
- `mghformat`
- `tmpdirs`
- `testing`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign v = np.arange(...)

```python
v = np.arange(120)
```

**Verification:**
```python
assert_equal(h['version'], 1)
```

### Step 2: Assign v = v.reshape.astype(...)

```python
v = v.reshape((5, 4, 3, 2)).astype(np.float32)
```

**Verification:**
```python
assert_equal(h['type'], 3)
```

### Step 3: Assign img = MGHImage(...)

```python
img = MGHImage(v, v2r)
```

**Verification:**
```python
assert_equal(h['dof'], 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(h['version'], 1)
```

**Verification:**
```python
assert_equal(h['goodRASFlag'], 1)
```

### Step 5: Call assert_equal()

```python
assert_equal(h['type'], 3)
```

**Verification:**
```python
assert_array_equal(h['dims'], [5, 4, 3, 2])
```

### Step 6: Call assert_equal()

```python
assert_equal(h['dof'], 0)
```

**Verification:**
```python
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
```

### Step 7: Call assert_equal()

```python
assert_equal(h['goodRASFlag'], 1)
```

**Verification:**
```python
assert_array_almost_equal(h.get_vox2ras(), v2r)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(h['dims'], [5, 4, 3, 2])
```

**Verification:**
```python
assert_almost_equal(dat, v, 7)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h.get_vox2ras(), v2r)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(dat, v, 7)
```

### Step 12: Call save()

```python
save(img, 'tmpsave.mgz')
```

### Step 13: Assign mgz = load(...)

```python
mgz = load('tmpsave.mgz')
```

### Step 14: Assign h = mgz.get_header(...)

```python
h = mgz.get_header()
```

### Step 15: Assign dat = mgz.get_data(...)

```python
dat = mgz.get_data()
```


## Complete Example

```python
# Workflow
v = np.arange(120)
v = v.reshape((5, 4, 3, 2)).astype(np.float32)
img = MGHImage(v, v2r)
with InTemporaryDirectory():
    save(img, 'tmpsave.mgz')
    mgz = load('tmpsave.mgz')
    h = mgz.get_header()
    dat = mgz.get_data()
    del mgz
assert_equal(h['version'], 1)
assert_equal(h['type'], 3)
assert_equal(h['dof'], 0)
assert_equal(h['goodRASFlag'], 1)
assert_array_equal(h['dims'], [5, 4, 3, 2])
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
assert_array_almost_equal(h.get_vox2ras(), v2r)
assert_almost_equal(dat, v, 7)
```

## Next Steps


---

*Source: test_mghformat.py:49 | Complexity: Advanced | Last updated: 2026-05-18*