# How To: Decimate Surface Vtk

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test triangular surface decimation.

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
# Fixtures: n_tri
```

## Step-by-Step Guide

### Step 1: 'Test triangular surface decimation.'

```python
'Test triangular surface decimation.'
```

**Verification:**
```python
assert len(this_tris) in want
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pyvista')
```

### Step 3: Assign points = np.array(...)

```python
points = np.array([[-0.00686118, -0.1036986, 0.0261517], [-0.00713948, -0.10370162, 0.02614874], [-0.00686208, -0.10368247, 0.02588313], [-0.00713987, -0.10368724, 0.02587745]])
```

### Step 4: Assign tris = np.array(...)

```python
tris = np.array([[0, 1, 2], [1, 2, 3], [0, 3, 1], [1, 2, 0]])
```

### Step 5: Assign unknown = decimate_surface(...)

```python
_, this_tris = decimate_surface(points, tris, n_tri)
```

### Step 6: Assign want = value

```python
want = (n_tri, n_tri - 1)
```

**Verification:**
```python
assert len(this_tris) in want
```

### Step 7: Assign nirvana = 5

```python
nirvana = 5
```

### Step 8: Assign tris = np.array(...)

```python
tris = np.array([[0, 1, 2], [1, 2, 3], [0, 3, 1], [1, 2, nirvana]])
```

### Step 9: Assign want = value

```python
want = want + (1,)
```

### Step 10: Call decimate_surface()

```python
decimate_surface(points, tris, len(tris) + 1)
```

### Step 11: Call decimate_surface()

```python
decimate_surface(points, tris, n_tri)
```


## Complete Example

```python
# Setup
# Fixtures: n_tri

# Workflow
'Test triangular surface decimation.'
pytest.importorskip('pyvista')
points = np.array([[-0.00686118, -0.1036986, 0.0261517], [-0.00713948, -0.10370162, 0.02614874], [-0.00686208, -0.10368247, 0.02588313], [-0.00713987, -0.10368724, 0.02587745]])
tris = np.array([[0, 1, 2], [1, 2, 3], [0, 3, 1], [1, 2, 0]])
_, this_tris = decimate_surface(points, tris, n_tri)
want = (n_tri, n_tri - 1)
if n_tri == 3:
    want = want + (1,)
assert len(this_tris) in want
with pytest.raises(ValueError, match='exceeds number of original'):
    decimate_surface(points, tris, len(tris) + 1)
nirvana = 5
tris = np.array([[0, 1, 2], [1, 2, 3], [0, 3, 1], [1, 2, nirvana]])
with pytest.raises(ValueError, match='undefined points'):
    decimate_surface(points, tris, n_tri)
```

## Next Steps


---

*Source: test_surface.py:171 | Complexity: Advanced | Last updated: 2026-05-18*