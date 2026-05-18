# How To: Quad Geometry

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Test IO of freesurfer quad files.

## Prerequisites

**Required Modules:**
- `getpass`
- `hashlib`
- `os`
- `struct`
- `time`
- `unittest`
- `os.path`
- `os.path`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileslice`
- `testing`
- `tests.nibabel_data`
- `tmpdirs`
- `io`


## Step-by-Step Guide

### Step 1: 'Test IO of freesurfer quad files.'

```python
'Test IO of freesurfer quad files.'
```

**Verification:**
```python
assert 0 == faces.min()
```

### Step 2: Assign new_quad = pjoin(...)

```python
new_quad = pjoin(get_nibabel_data(), 'nitest-freesurfer', 'subjects', 'bert', 'surf', 'lh.inflated.nofix')
```

**Verification:**
```python
assert coords.shape[0] == faces.max() + 1
```

### Step 3: Assign unknown = read_geometry(...)

```python
coords, faces = read_geometry(new_quad)
```

**Verification:**
```python
assert np.array_equal(coords, coords2)
```

### Step 4: Assign new_path = 'test'

```python
new_path = 'test'
```

**Verification:**
```python
assert np.array_equal(faces, faces2)
```

### Step 5: Call write_geometry()

```python
write_geometry(new_path, coords, faces)
```

### Step 6: Assign unknown = read_geometry(...)

```python
coords2, faces2 = read_geometry(new_path)
```

**Verification:**
```python
assert np.array_equal(coords, coords2)
```


## Complete Example

```python
# Workflow
'Test IO of freesurfer quad files.'
new_quad = pjoin(get_nibabel_data(), 'nitest-freesurfer', 'subjects', 'bert', 'surf', 'lh.inflated.nofix')
coords, faces = read_geometry(new_quad)
assert 0 == faces.min()
assert coords.shape[0] == faces.max() + 1
with InTemporaryDirectory():
    new_path = 'test'
    write_geometry(new_path, coords, faces)
    coords2, faces2 = read_geometry(new_path)
    assert np.array_equal(coords, coords2)
    assert np.array_equal(faces, faces2)
```

## Next Steps


---

*Source: test_io.py:119 | Complexity: Advanced | Last updated: 2026-05-18*