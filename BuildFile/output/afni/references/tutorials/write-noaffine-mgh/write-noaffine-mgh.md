# How To: Write Noaffine Mgh

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test write noaffine mgh

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

### Step 1: Assign v = np.ones.astype(...)

```python
v = np.ones((7, 13, 3, 22)).astype(np.uint8)
```

**Verification:**
```python
assert_equal(h['version'], 1)
```

### Step 2: Assign img = MGHImage(...)

```python
img = MGHImage(v, None)
```

**Verification:**
```python
assert_equal(h['type'], 0)
```

### Step 3: Call assert_equal()

```python
assert_equal(h['version'], 1)
```

**Verification:**
```python
assert_equal(h['dof'], 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(h['type'], 0)
```

**Verification:**
```python
assert_equal(h['goodRASFlag'], 1)
```

### Step 5: Call assert_equal()

```python
assert_equal(h['dof'], 0)
```

**Verification:**
```python
assert_array_equal(h['dims'], [7, 13, 3, 22])
```

### Step 6: Call assert_equal()

```python
assert_equal(h['goodRASFlag'], 1)
```

**Verification:**
```python
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(h['dims'], [7, 13, 3, 22])
```

**Verification:**
```python
assert_array_almost_equal(h['Mdc'], ex_mdc)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
```

**Verification:**
```python
assert_array_almost_equal(h['Pxyz_c'], ex_pxyzc)
```

### Step 9: Assign ex_mdc = np.array(...)

```python
ex_mdc = np.array([[-1, 0, 0], [0, 0, -1], [0, 1, 0]], dtype=np.float32)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h['Mdc'], ex_mdc)
```

### Step 11: Assign ex_pxyzc = np.array(...)

```python
ex_pxyzc = np.array([0, 0, 0], dtype=np.float32)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h['Pxyz_c'], ex_pxyzc)
```

### Step 13: Call save()

```python
save(img, 'tmpsave.mgz')
```

### Step 14: Assign mgz = load(...)

```python
mgz = load('tmpsave.mgz')
```

### Step 15: Assign h = mgz.get_header(...)

```python
h = mgz.get_header()
```


## Complete Example

```python
# Workflow
v = np.ones((7, 13, 3, 22)).astype(np.uint8)
img = MGHImage(v, None)
with InTemporaryDirectory():
    save(img, 'tmpsave.mgz')
    mgz = load('tmpsave.mgz')
    h = mgz.get_header()
    del mgz
assert_equal(h['version'], 1)
assert_equal(h['type'], 0)
assert_equal(h['dof'], 0)
assert_equal(h['goodRASFlag'], 1)
assert_array_equal(h['dims'], [7, 13, 3, 22])
assert_array_almost_equal(h['mrparms'], [0.0, 0.0, 0.0, 0.0])
ex_mdc = np.array([[-1, 0, 0], [0, 0, -1], [0, 1, 0]], dtype=np.float32)
assert_array_almost_equal(h['Mdc'], ex_mdc)
ex_pxyzc = np.array([0, 0, 0], dtype=np.float32)
assert_array_almost_equal(h['Pxyz_c'], ex_pxyzc)
```

## Next Steps


---

*Source: test_mghformat.py:75 | Complexity: Advanced | Last updated: 2026-05-18*