# How To: Bem Model Topology

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test BEM model topological checks.

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

### Step 1: 'Test BEM model topological checks.'

```python
'Test BEM model topological checks.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Call makedirs()

```python
makedirs(tmp_path / 'foo' / 'bem')
```

### Step 4: Call _chmod_rw_R()

```python
_chmod_rw_R(tmp_path)
```

### Step 5: Assign outer_fname = value

```python
outer_fname = tmp_path / 'foo' / 'bem' / 'outer_skull.surf'
```

### Step 6: Assign unknown = read_surface(...)

```python
rr, tris = read_surface(outer_fname)
```

### Step 7: Assign tris = value

```python
tris = tris[:-1]
```

### Step 8: Call write_surface()

```python
write_surface(outer_fname, rr, tris[:-1], overwrite=True)
```

### Step 9: Assign rr_bad = np.concatenate(...)

```python
rr_bad = np.concatenate([rr, np.mean(rr, axis=0, keepdims=True)], axis=0)
```

### Step 10: Call write_surface()

```python
write_surface(outer_fname, rr_bad, tris, overwrite=True)
```

### Step 11: Call copy()

```python
copy(subjects_dir / 'sample' / 'bem' / fname, tmp_path / 'foo' / 'bem' / fname)
```

### Step 12: Call make_bem_model()

```python
make_bem_model('foo', None, subjects_dir=tmp_path)
```

### Step 13: Call make_bem_model()

```python
make_bem_model('foo', None, subjects_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test BEM model topological checks.'
pytest.importorskip('nibabel')
makedirs(tmp_path / 'foo' / 'bem')
for fname in ('inner_skull', 'outer_skull', 'outer_skin'):
    fname += '.surf'
    copy(subjects_dir / 'sample' / 'bem' / fname, tmp_path / 'foo' / 'bem' / fname)
_chmod_rw_R(tmp_path)
outer_fname = tmp_path / 'foo' / 'bem' / 'outer_skull.surf'
rr, tris = read_surface(outer_fname)
tris = tris[:-1]
write_surface(outer_fname, rr, tris[:-1], overwrite=True)
with pytest.raises(RuntimeError, match='Surface outer skull is not compl'):
    make_bem_model('foo', None, subjects_dir=tmp_path)
rr_bad = np.concatenate([rr, np.mean(rr, axis=0, keepdims=True)], axis=0)
write_surface(outer_fname, rr_bad, tris, overwrite=True)
with pytest.raises(ValueError, match='Surface outer skull.*triangles'):
    make_bem_model('foo', None, subjects_dir=tmp_path)
```

## Next Steps


---

*Source: test_bem.py:224 | Complexity: Advanced | Last updated: 2026-05-18*