# How To: Marching Cubes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test creating surfaces via marching cubes.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: dtype, value, smooth, order
```

## Step-by-Step Guide

### Step 1: 'Test creating surfaces via marching cubes.'

```python
'Test creating surfaces via marching cubes.'
```

**Verification:**
```python
assert len(out) == 1
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pyvista')
```

**Verification:**
```python
assert_allclose(verts.sum(axis=0), [14700, 14700, 14700], rtol=rtol)
```

### Step 3: Assign data = np.zeros(...)

```python
data = np.zeros((50, 50, 50), dtype=dtype, order=order)
```

**Verification:**
```python
assert tri_sum in ([350588, 360865, 363402], [350408, 359867, 364089])
```

### Step 4: Assign unknown = value

```python
data[20:30, 20:30, 20:30] = value
```

**Verification:**
```python
assert np.linalg.norm(verts - np.array([25, 25, 25]), axis=1).min() > 4
```

### Step 5: Assign level = value

```python
level = [value]
```

### Step 6: Assign out = _marching_cubes(...)

```python
out = _marching_cubes(data, level, smooth=smooth)
```

**Verification:**
```python
assert len(out) == 1
```

### Step 7: Assign unknown = value

```python
verts, triangles = out[0]
```

### Step 8: Assign rtol = value

```python
rtol = 0.01 if smooth else 1e-09
```

### Step 9: Call assert_allclose()

```python
assert_allclose(verts.sum(axis=0), [14700, 14700, 14700], rtol=rtol)
```

### Step 10: Assign tri_sum = triangles.sum.tolist(...)

```python
tri_sum = triangles.sum(axis=0).tolist()
```

**Verification:**
```python
assert tri_sum in ([350588, 360865, 363402], [350408, 359867, 364089])
```

### Step 11: Assign unknown = 0

```python
data[24:27, 24:27, 24:27] = 0
```

### Step 12: Assign unknown = value

```python
verts, triangles = _marching_cubes(data, level, smooth=smooth, fill_hole_size=2)[0]
```

**Verification:**
```python
assert np.linalg.norm(verts - np.array([25, 25, 25]), axis=1).min() > 4
```

### Step 13: Call _marching_cubes()

```python
_marching_cubes(data, ['foo'])
```

### Step 14: Call _marching_cubes()

```python
_marching_cubes(data, [[1]])
```

### Step 15: Call _marching_cubes()

```python
_marching_cubes(data, [1.0])
```

### Step 16: Call _marching_cubes()

```python
_marching_cubes(data, [1], smooth=1.0)
```

### Step 17: Call _marching_cubes()

```python
_marching_cubes(data[0], [1])
```


## Complete Example

```python
# Setup
# Fixtures: dtype, value, smooth, order

# Workflow
'Test creating surfaces via marching cubes.'
pytest.importorskip('pyvista')
data = np.zeros((50, 50, 50), dtype=dtype, order=order)
data[20:30, 20:30, 20:30] = value
level = [value]
out = _marching_cubes(data, level, smooth=smooth)
assert len(out) == 1
verts, triangles = out[0]
rtol = 0.01 if smooth else 1e-09
assert_allclose(verts.sum(axis=0), [14700, 14700, 14700], rtol=rtol)
tri_sum = triangles.sum(axis=0).tolist()
assert tri_sum in ([350588, 360865, 363402], [350408, 359867, 364089])
data[24:27, 24:27, 24:27] = 0
verts, triangles = _marching_cubes(data, level, smooth=smooth, fill_hole_size=2)[0]
assert np.linalg.norm(verts - np.array([25, 25, 25]), axis=1).min() > 4
with pytest.raises(TypeError, match='1D array-like'):
    _marching_cubes(data, ['foo'])
with pytest.raises(TypeError, match='1D array-like'):
    _marching_cubes(data, [[1]])
with pytest.raises(TypeError, match='1D array-like'):
    _marching_cubes(data, [1.0])
with pytest.raises(ValueError, match='must be between 0'):
    _marching_cubes(data, [1], smooth=1.0)
with pytest.raises(ValueError, match='3D data'):
    _marching_cubes(data[0], [1])
```

## Next Steps


---

*Source: test_surface.py:252 | Complexity: Advanced | Last updated: 2026-05-18*