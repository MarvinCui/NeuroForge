# How To: Unpack Surface

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unpack surface

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.viz.horizon.util`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 4))
```

### Step 2: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 3))
```

### Step 3: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 3))
```

### Step 4: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 4))
```

### Step 5: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 3))
```

### Step 6: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 3))
```

### Step 7: Assign unknown = unpack_surface(...)

```python
v, f, fname = unpack_surface((vertices, faces, '/test/filename.pial'))
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(vertices, v)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(faces, f)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal('/test/filename.pial', fname)
```

### Step 11: Call unpack_surface()

```python
unpack_surface((vertices, faces))
```

### Step 12: Call unpack_surface()

```python
unpack_surface((vertices, faces, '/test/filename.pial'))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
vertices = rng.random((100, 4))
faces = rng.integers(0, 100, size=(100, 3))
with npt.assert_raises(ValueError):
    unpack_surface((vertices, faces))
vertices = rng.random((100, 3))
faces = rng.integers(0, 100, size=(100, 4))
with npt.assert_raises(ValueError):
    unpack_surface((vertices, faces, '/test/filename.pial'))
vertices = rng.random((100, 3))
faces = rng.integers(0, 100, size=(100, 3))
v, f, fname = unpack_surface((vertices, faces, '/test/filename.pial'))
npt.assert_equal(vertices, v)
npt.assert_equal(faces, f)
npt.assert_equal('/test/filename.pial', fname)
```

## Next Steps


---

*Source: test_util.py:119 | Complexity: Advanced | Last updated: 2026-05-18*