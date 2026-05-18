# How To: Read Mgh

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read mgh

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

### Step 1: Assign mgz_path = os.path.join(...)

```python
mgz_path = os.path.join(data_path, 'test.mgz')
```

**Verification:**
```python
assert_equal(h['version'], 1)
```

### Step 2: Assign mgz = load(...)

```python
mgz = load(mgz_path)
```

**Verification:**
```python
assert_equal(h['type'], 3)
```

### Step 3: Assign h = mgz.get_header(...)

```python
h = mgz.get_header()
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
assert_array_equal(h['dims'], [3, 4, 5, 2])
```

### Step 6: Call assert_equal()

```python
assert_equal(h['dof'], 0)
```

**Verification:**
```python
assert_array_almost_equal(h['mrparms'], [2.0, 0.0, 0.0, 0.0])
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
assert_array_equal(h['dims'], [3, 4, 5, 2])
```

**Verification:**
```python
assert_almost_equal(v[1, 2, 3, 0], -0.3047, 4)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h['mrparms'], [2.0, 0.0, 0.0, 0.0])
```

**Verification:**
```python
assert_almost_equal(v[1, 2, 3, 1], 0.0018, 4)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(h.get_vox2ras(), v2r)
```

### Step 11: Assign v = mgz.get_data(...)

```python
v = mgz.get_data()
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(v[1, 2, 3, 0], -0.3047, 4)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(v[1, 2, 3, 1], 0.0018, 4)
```


## Complete Example

```python
# Workflow
mgz_path = os.path.join(data_path, 'test.mgz')
mgz = load(mgz_path)
h = mgz.get_header()
assert_equal(h['version'], 1)
assert_equal(h['type'], 3)
assert_equal(h['dof'], 0)
assert_equal(h['goodRASFlag'], 1)
assert_array_equal(h['dims'], [3, 4, 5, 2])
assert_array_almost_equal(h['mrparms'], [2.0, 0.0, 0.0, 0.0])
assert_array_almost_equal(h.get_vox2ras(), v2r)
v = mgz.get_data()
assert_almost_equal(v[1, 2, 3, 0], -0.3047, 4)
assert_almost_equal(v[1, 2, 3, 1], 0.0018, 4)
```

## Next Steps


---

*Source: test_mghformat.py:25 | Complexity: Advanced | Last updated: 2026-05-18*