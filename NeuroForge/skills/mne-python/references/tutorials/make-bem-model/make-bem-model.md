# How To: Make Bem Model

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test BEM model creation from Python with I/O.

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
# Fixtures: tmp_path, kwargs, fname
```

## Step-by-Step Guide

### Step 1: 'Test BEM model creation from Python with I/O.'

```python
'Test BEM model creation from Python with I/O.'
```

**Verification:**
```python
assert 'distance' not in log
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert re.search('surfaces is approximately *3\\.4 mm', log) is not None
```

### Step 3: Assign fname_temp = value

```python
fname_temp = tmp_path / 'temp-bem.fif'
```

**Verification:**
```python
assert re.search('inner skull CM is *0\\.65 *-9\\.62 *43\\.85 mm', log) is not None
```

### Step 4: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert re.search('inner skull CM is *0\\.65 *-9\\.62 *43\\.85 mm', log) is not None
```

### Step 5: Assign model_c = read_bem_surfaces(...)

```python
model_c = read_bem_surfaces(fname)
```

### Step 6: Call _compare_bem_surfaces()

```python
_compare_bem_surfaces(model, model_c)
```

### Step 7: Call write_bem_surfaces()

```python
write_bem_surfaces(fname_temp, model)
```

### Step 8: Assign model_read = read_bem_surfaces(...)

```python
model_read = read_bem_surfaces(fname_temp)
```

### Step 9: Call _compare_bem_surfaces()

```python
_compare_bem_surfaces(model, model_c)
```

### Step 10: Call _compare_bem_surfaces()

```python
_compare_bem_surfaces(model_read, model_c)
```

### Step 11: Assign model = make_bem_model(...)

```python
model = make_bem_model('sample', ico=2, subjects_dir=subjects_dir, verbose=True, **kwargs)
```

**Verification:**
```python
assert 'distance' not in log
```

### Step 12: Call make_bem_model()

```python
make_bem_model('sample', 4, [0.3, 0.006], subjects_dir=subjects_dir)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, kwargs, fname

# Workflow
'Test BEM model creation from Python with I/O.'
pytest.importorskip('nibabel')
fname_temp = tmp_path / 'temp-bem.fif'
with catch_logging() as log:
    model = make_bem_model('sample', ico=2, subjects_dir=subjects_dir, verbose=True, **kwargs)
log = log.getvalue()
if len(kwargs.get('conductivity', (0, 0, 0))) == 1:
    assert 'distance' not in log
else:
    assert re.search('surfaces is approximately *3\\.4 mm', log) is not None
assert re.search('inner skull CM is *0\\.65 *-9\\.62 *43\\.85 mm', log) is not None
model_c = read_bem_surfaces(fname)
_compare_bem_surfaces(model, model_c)
write_bem_surfaces(fname_temp, model)
model_read = read_bem_surfaces(fname_temp)
_compare_bem_surfaces(model, model_c)
_compare_bem_surfaces(model_read, model_c)
with pytest.raises(ValueError, match='conductivity must be'):
    make_bem_model('sample', 4, [0.3, 0.006], subjects_dir=subjects_dir)
```

## Next Steps


---

*Source: test_bem.py:198 | Complexity: Advanced | Last updated: 2026-05-18*