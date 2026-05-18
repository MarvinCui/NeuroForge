# How To: Other Volume Source Spaces

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test setting up other volume source spaces.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test setting up other volume source spaces.'

```python
'Test setting up other volume source spaces.'
```

**Verification:**
```python
assert len(src_new[0]['vertno']) == 7497
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert len(src) == 1
```

### Step 3: Assign temp_name = value

```python
temp_name = tmp_path / 'temp-src.fif'
```

**Verification:**
```python
assert len(src_new) == 1
```

### Step 4: Call run_subprocess()

```python
run_subprocess(['mne_volume_source_space', '--grid', '7.0', '--src', temp_name, '--mri', fname_mri])
```

**Verification:**
```python
assert src[0]['inuse'].sum() == 7497
```

### Step 5: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(temp_name)
```

**Verification:**
```python
assert len(src[0]['vertno']) == 7497
```

### Step 6: Assign sphere = value

```python
sphere = (0.0, 0.0, 0.0, 0.09)
```

**Verification:**
```python
assert src[0]['nuse'] == 7497
```

### Step 7: Assign src_new = setup_volume_source_space(...)

```python
src_new = setup_volume_source_space(None, pos=7.0, mri=fname_mri, subjects_dir=subjects_dir, sphere=sphere)
```

**Verification:**
```python
assert 'volume, shape' in repr(src)
```

### Step 8: Assign good_mask = np.isin(...)

```python
good_mask = np.isin(src[0]['vertno'], src_new[0]['vertno'])
```

### Step 9: Assign unknown = 0

```python
src[0]['inuse'][src[0]['vertno'][~good_mask]] = 0
```

**Verification:**
```python
assert src[0]['inuse'].sum() == 7497
```

### Step 10: Assign unknown = value

```python
src[0]['vertno'] = src[0]['vertno'][good_mask]
```

**Verification:**
```python
assert len(src[0]['vertno']) == 7497
```

### Step 11: Assign unknown = len(...)

```python
src[0]['nuse'] = len(src[0]['vertno'])
```

**Verification:**
```python
assert src[0]['nuse'] == 7497
```

### Step 12: Call _compare_source_spaces()

```python
_compare_source_spaces(src_new, src, mode='approx')
```

**Verification:**
```python
assert 'volume, shape' in repr(src)
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, setup_volume_source_space, 'sample', pos=7.0, sphere=[1.0, 1.0], mri=fname_mri, subjects_dir=subjects_dir)
```

### Step 14: Call run_subprocess()

```python
run_subprocess(['mne_volume_source_space', '--grid', '7.0', '--src', temp_name])
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, read_source_spaces, temp_name)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test setting up other volume source spaces.'
pytest.importorskip('nibabel')
temp_name = tmp_path / 'temp-src.fif'
run_subprocess(['mne_volume_source_space', '--grid', '7.0', '--src', temp_name, '--mri', fname_mri])
src = read_source_spaces(temp_name)
sphere = (0.0, 0.0, 0.0, 0.09)
src_new = setup_volume_source_space(None, pos=7.0, mri=fname_mri, subjects_dir=subjects_dir, sphere=sphere)
assert len(src_new[0]['vertno']) == 7497
assert len(src) == 1
assert len(src_new) == 1
good_mask = np.isin(src[0]['vertno'], src_new[0]['vertno'])
src[0]['inuse'][src[0]['vertno'][~good_mask]] = 0
assert src[0]['inuse'].sum() == 7497
src[0]['vertno'] = src[0]['vertno'][good_mask]
assert len(src[0]['vertno']) == 7497
src[0]['nuse'] = len(src[0]['vertno'])
assert src[0]['nuse'] == 7497
_compare_source_spaces(src_new, src, mode='approx')
assert 'volume, shape' in repr(src)
del src
del src_new
pytest.raises(ValueError, setup_volume_source_space, 'sample', pos=7.0, sphere=[1.0, 1.0], mri=fname_mri, subjects_dir=subjects_dir)
run_subprocess(['mne_volume_source_space', '--grid', '7.0', '--src', temp_name])
pytest.raises(ValueError, read_source_spaces, temp_name)
```

## Next Steps


---

*Source: test_source_space.py:383 | Complexity: Advanced | Last updated: 2026-05-18*