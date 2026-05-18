# How To: Make Sphere Model

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test making a sphere model.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test making a sphere model.'

```python
'Test making a sphere model.'
```

**Verification:**
```python
assert ' RV = ' in log
```

### Step 2: Assign info = read_info(...)

```python
info = read_info(fname_raw)
```

**Verification:**
```python
assert val < 0.01
```

### Step 3: Call pytest.raises()

```python
pytest.raises(ValueError, make_sphere_model, 'foo', 'auto', info)
```

**Verification:**
```python
assert '3 layers' in repr(bem)
```

### Step 4: Call pytest.raises()

```python
pytest.raises(ValueError, make_sphere_model, 'auto', 'auto', None)
```

**Verification:**
```python
assert 'Sphere ' in repr(bem)
```

### Step 5: Call pytest.raises()

```python
pytest.raises(ValueError, make_sphere_model, 'auto', 'auto', info, relative_radii=(), sigmas=())
```

**Verification:**
```python
assert ' mm' in repr(bem)
```

### Step 6: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'no layers' in repr(bem)
```

### Step 7: Assign bem = make_sphere_model(...)

```python
bem = make_sphere_model('auto', None, info)
```

**Verification:**
```python
assert 'Sphere ' in repr(bem)
```

### Step 8: Call make_sphere_model()

```python
make_sphere_model('auto', 'auto', info, relative_radii=(1,))
```

### Step 9: Assign bem = make_sphere_model(...)

```python
bem = make_sphere_model('auto', 'auto', info, verbose=True)
```

### Step 10: Call make_sphere_model()

```python
make_sphere_model(sigmas=(0.33,), relative_radii=(1.0,))
```

### Step 11: Assign val = float(...)

```python
val = float(line.split()[-2])
```

**Verification:**
```python
assert val < 0.01
```


## Complete Example

```python
# Workflow
'Test making a sphere model.'
info = read_info(fname_raw)
pytest.raises(ValueError, make_sphere_model, 'foo', 'auto', info)
pytest.raises(ValueError, make_sphere_model, 'auto', 'auto', None)
pytest.raises(ValueError, make_sphere_model, 'auto', 'auto', info, relative_radii=(), sigmas=())
with pytest.raises(ValueError, match='relative_radii.*must match.*sigmas'):
    make_sphere_model('auto', 'auto', info, relative_radii=(1,))
with catch_logging() as log:
    bem = make_sphere_model('auto', 'auto', info, verbose=True)
log = log.getvalue()
assert ' RV = ' in log
for line in log.split('\n'):
    if ' RV = ' in line:
        val = float(line.split()[-2])
        assert val < 0.01
        break
assert '3 layers' in repr(bem)
assert 'Sphere ' in repr(bem)
assert ' mm' in repr(bem)
bem = make_sphere_model('auto', None, info)
assert 'no layers' in repr(bem)
assert 'Sphere ' in repr(bem)
with pytest.raises(ValueError, match='at least 2 sigmas.*head_radius'):
    make_sphere_model(sigmas=(0.33,), relative_radii=(1.0,))
```

## Next Steps


---

*Source: test_bem.py:153 | Complexity: Advanced | Last updated: 2026-05-18*