# How To: Vertex To Mni Fs Nibabel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test equivalence of vert_to_mni for nibabel and freesurfer.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._freesurfer`
- `mne.datasets`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test equivalence of vert_to_mni for nibabel and freesurfer.'

```python
'Test equivalence of vert_to_mni for nibabel and freesurfer.'
```

**Verification:**
```python
assert_allclose(coords, coords_2, atol=0.1)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Assign n_check = 1000

```python
n_check = 1000
```

### Step 4: Assign subject = 'sample'

```python
subject = 'sample'
```

### Step 5: Assign vertices = rng.randint(...)

```python
vertices = rng.randint(0, 100000, n_check)
```

### Step 6: Assign hemis = rng.randint(...)

```python
hemis = rng.randint(0, 1, n_check)
```

### Step 7: Assign coords = vertex_to_mni(...)

```python
coords = vertex_to_mni(vertices, hemis, subject, subjects_dir)
```

### Step 8: Assign read_mri = value

```python
read_mri = mne._freesurfer._read_mri_info
```

### Step 9: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne._freesurfer, '_read_mri_info', lambda *args, **kwargs: read_mri(*args, use_nibabel=True, **kwargs))
```

### Step 10: Assign coords_2 = vertex_to_mni(...)

```python
coords_2 = vertex_to_mni(vertices, hemis, subject, subjects_dir)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(coords, coords_2, atol=0.1)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test equivalence of vert_to_mni for nibabel and freesurfer.'
pytest.importorskip('nibabel')
n_check = 1000
subject = 'sample'
vertices = rng.randint(0, 100000, n_check)
hemis = rng.randint(0, 1, n_check)
coords = vertex_to_mni(vertices, hemis, subject, subjects_dir)
read_mri = mne._freesurfer._read_mri_info
monkeypatch.setattr(mne._freesurfer, '_read_mri_info', lambda *args, **kwargs: read_mri(*args, use_nibabel=True, **kwargs))
coords_2 = vertex_to_mni(vertices, hemis, subject, subjects_dir)
assert_allclose(coords, coords_2, atol=0.1)
```

## Next Steps


---

*Source: test_freesurfer.py:111 | Complexity: Advanced | Last updated: 2026-05-18*