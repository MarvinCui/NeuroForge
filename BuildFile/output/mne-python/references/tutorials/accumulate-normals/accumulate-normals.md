# How To: Accumulate Normals

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test efficient normal accumulation for surfaces.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test efficient normal accumulation for surfaces.'

```python
'Test efficient normal accumulation for surfaces.'
```

**Verification:**
```python
assert_allclose(nn, this['nn'], rtol=1e-07, atol=1e-07)
```

### Step 2: Assign n_pts = int(...)

```python
n_pts = int(160000.0)
```

### Step 3: Assign n_tris = int(...)

```python
n_tris = int(320000.0)
```

### Step 4: Assign tris = unknown.astype(...)

```python
tris = (rng.rand(n_tris, 1) * (n_pts - 2)).astype(int)
```

### Step 5: Assign tris = value

```python
tris = np.c_[tris, tris + 1, tris + 2]
```

### Step 6: Assign tri_nn = rng.rand(...)

```python
tri_nn = rng.rand(n_tris, 3)
```

### Step 7: Assign this = dict(...)

```python
this = dict(tris=tris, np=n_pts, ntri=n_tris, tri_nn=tri_nn)
```

### Step 8: Assign unknown = np.zeros(...)

```python
this['nn'] = np.zeros((this['np'], 3))
```

### Step 9: Assign nn = _accumulate_normals(...)

```python
nn = _accumulate_normals(this['tris'], this['tri_nn'], this['np'])
```

### Step 10: Call assert_allclose()

```python
assert_allclose(nn, this['nn'], rtol=1e-07, atol=1e-07)
```

### Step 11: Assign verts = value

```python
verts = this['tris'][p]
```


## Complete Example

```python
# Workflow
'Test efficient normal accumulation for surfaces.'
n_pts = int(160000.0)
n_tris = int(320000.0)
tris = (rng.rand(n_tris, 1) * (n_pts - 2)).astype(int)
tris = np.c_[tris, tris + 1, tris + 2]
tri_nn = rng.rand(n_tris, 3)
this = dict(tris=tris, np=n_pts, ntri=n_tris, tri_nn=tri_nn)
this['nn'] = np.zeros((this['np'], 3))
for p in range(this['ntri']):
    verts = this['tris'][p]
    this['nn'][verts, :] += this['tri_nn'][p, :]
nn = _accumulate_normals(this['tris'], this['tri_nn'], this['np'])
assert_allclose(nn, this['nn'], rtol=1e-07, atol=1e-07)
```

## Next Steps


---

*Source: test_source_space.py:459 | Complexity: Advanced | Last updated: 2026-05-18*