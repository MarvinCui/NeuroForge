# How To: Io Head Bem

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading and writing of defective head surfaces.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `copy`
- `os`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`
- `h5py`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading and writing of defective head surfaces.'

```python
'Test reading and writing of defective head surfaces.'
```

**Verification:**
```python
assert head['id'] == head_defect['id'] == FIFF.FIFFV_BEM_SURF_ID_HEAD
```

### Step 2: Assign head = value

```python
head = read_bem_surfaces(fname_dense_head)[0]
```

**Verification:**
```python
assert np.allclose(head['rr'], head_defect['rr'])
```

### Step 3: Assign fname_defect = value

```python
fname_defect = tmp_path / 'temp-head-defect.fif'
```

**Verification:**
```python
assert np.allclose(head['tris'], head_defect['tris'])
```

### Step 4: Assign unknown = np.array(...)

```python
head['rr'][0] = np.array([-0.01487014, -0.04563854, -0.12660208])
```

### Step 5: Assign unknown = np.array(...)

```python
head['tris'][0] = np.array([21919, 21918, 21907])
```

**Verification:**
```python
assert head['id'] == head_defect['id'] == FIFF.FIFFV_BEM_SURF_ID_HEAD
```

### Step 6: Call write_head_bem()

```python
write_head_bem(fname_defect, head['rr'], head['tris'])
```

### Step 7: Call write_head_bem()

```python
write_head_bem(fname_defect, head['rr'], head['tris'], on_defects='warn')
```

### Step 8: Call read_bem_surfaces()

```python
read_bem_surfaces(fname_defect)
```

### Step 9: Assign head_defect = value

```python
head_defect = read_bem_surfaces(fname_defect, on_defects='warn')[0]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading and writing of defective head surfaces.'
head = read_bem_surfaces(fname_dense_head)[0]
fname_defect = tmp_path / 'temp-head-defect.fif'
head['rr'][0] = np.array([-0.01487014, -0.04563854, -0.12660208])
head['tris'][0] = np.array([21919, 21918, 21907])
with pytest.raises(ValueError, match='topological defects:'):
    write_head_bem(fname_defect, head['rr'], head['tris'])
with _record_warnings(), pytest.warns(RuntimeWarning, match='topological defects:'):
    write_head_bem(fname_defect, head['rr'], head['tris'], on_defects='warn')
with pytest.raises(ValueError, match='topological defects:'):
    read_bem_surfaces(fname_defect)
with _record_warnings(), pytest.warns(RuntimeWarning, match='topological defects:'):
    head_defect = read_bem_surfaces(fname_defect, on_defects='warn')[0]
assert head['id'] == head_defect['id'] == FIFF.FIFFV_BEM_SURF_ID_HEAD
assert np.allclose(head['rr'], head_defect['rr'])
assert np.allclose(head['tris'], head_defect['tris'])
```

## Next Steps


---

*Source: test_bem.py:505 | Complexity: Advanced | Last updated: 2026-05-18*