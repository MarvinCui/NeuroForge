# How To: Read Source Spaces

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test reading of source space meshes.

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

### Step 1: 'Test reading of source space meshes.'

```python
'Test reading of source space meshes.'
```

**Verification:**
```python
assert lh_faces.min() == 0
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname, patch_stats=True)
```

**Verification:**
```python
assert lh_faces.max() == lh_points.shape[0] - 1
```

### Step 3: Assign lh_points = value

```python
lh_points = src[0]['rr']
```

**Verification:**
```python
assert lh_use_faces.min() >= 0
```

### Step 4: Assign lh_faces = value

```python
lh_faces = src[0]['tris']
```

**Verification:**
```python
assert lh_use_faces.max() <= lh_points.shape[0] - 1
```

### Step 5: Assign lh_use_faces = value

```python
lh_use_faces = src[0]['use_tris']
```

**Verification:**
```python
assert rh_faces.min() == 0
```

### Step 6: Assign rh_points = value

```python
rh_points = src[1]['rr']
```

**Verification:**
```python
assert rh_faces.max() == rh_points.shape[0] - 1
```

### Step 7: Assign rh_faces = value

```python
rh_faces = src[1]['tris']
```

**Verification:**
```python
assert rh_use_faces.min() >= 0
```

### Step 8: Assign rh_use_faces = value

```python
rh_use_faces = src[1]['use_tris']
```

**Verification:**
```python
assert rh_use_faces.max() <= rh_points.shape[0] - 1
```


## Complete Example

```python
# Workflow
'Test reading of source space meshes.'
src = read_source_spaces(fname, patch_stats=True)
lh_points = src[0]['rr']
lh_faces = src[0]['tris']
lh_use_faces = src[0]['use_tris']
rh_points = src[1]['rr']
rh_faces = src[1]['tris']
rh_use_faces = src[1]['use_tris']
assert lh_faces.min() == 0
assert lh_faces.max() == lh_points.shape[0] - 1
assert lh_use_faces.min() >= 0
assert lh_use_faces.max() <= lh_points.shape[0] - 1
assert rh_faces.min() == 0
assert rh_faces.max() == rh_points.shape[0] - 1
assert rh_use_faces.min() >= 0
assert rh_use_faces.max() <= rh_points.shape[0] - 1
```

## Next Steps


---

*Source: test_source_space.py:582 | Complexity: Advanced | Last updated: 2026-05-18*