# How To: Write Mgh

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test write mgh

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `openers`
- `spatialimages`
- `testing`
- `tests`
- `tests`
- `tmpdirs`
- `volumeutils`
- `wrapstruct`
- `mghformat`


## Step-by-Step Guide

### Step 1: Assign v = np.arange(...)

```python
v = np.arange(120)
```

**Verification:**
```python
assert h['version'] == 1
```

### Step 2: Assign v = v.reshape.astype(...)

```python
v = v.reshape((5, 4, 3, 2)).astype(np.float32)
```

**Verification:**
```python
assert h['type'] == 3
```

### Step 3: Assign img = MGHImage(...)

```python
img = MGHImage(v, v2r)
```

**Verification:**
```python
assert h['dof'] == 0
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(h['tr'], 0.0)
```

**Verification:**
```python
assert h['goodRASFlag'] == 1
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(h['flip_angle'], 0.0)
```

**Verification:**
```python
assert np.array_equal(h['dims'], [5, 4, 3, 2])
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(h['te'], 0.0)
```

**Verification:**
```python
assert_almost_equal(h['tr'], 0.0)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(h['ti'], 0.0)
```

**Verification:**
```python
assert_almost_equal(h['flip_angle'], 0.0)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(h['fov'], 0.0)
```

**Verification:**
```python
assert_almost_equal(h['te'], 0.0)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h.get_vox2ras(), v2r)
```

**Verification:**
```python
assert_almost_equal(h['ti'], 0.0)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(dat, v, 7)
```

**Verification:**
```python
assert_almost_equal(h['fov'], 0.0)
```

### Step 11: Call save()

```python
save(img, 'tmpsave.mgz')
```

**Verification:**
```python
assert_array_almost_equal(h.get_vox2ras(), v2r)
```

### Step 12: Assign mgz = load(...)

```python
mgz = load('tmpsave.mgz')
```

**Verification:**
```python
assert_almost_equal(dat, v, 7)
```

### Step 13: Assign h = value

```python
h = mgz.header
```

### Step 14: Assign dat = mgz.get_fdata(...)

```python
dat = mgz.get_fdata()
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
    h = mgz.header
    dat = mgz.get_fdata()
    del mgz
assert h['version'] == 1
assert h['type'] == 3
assert h['dof'] == 0
assert h['goodRASFlag'] == 1
assert np.array_equal(h['dims'], [5, 4, 3, 2])
assert_almost_equal(h['tr'], 0.0)
assert_almost_equal(h['flip_angle'], 0.0)
assert_almost_equal(h['te'], 0.0)
assert_almost_equal(h['ti'], 0.0)
assert_almost_equal(h['fov'], 0.0)
assert_array_almost_equal(h.get_vox2ras(), v2r)
assert_almost_equal(dat, v, 7)
```

## Next Steps


---

*Source: test_mghformat.py:95 | Complexity: Advanced | Last updated: 2026-05-18*