# How To: Make Field Map Eeg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test interpolation of EEG field onto head.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.polynomial`
- `numpy.testing`
- `scipy.interpolate`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.forward._field_interpolation`
- `mne.forward._lead_dots`
- `mne.forward._make_forward`
- `mne.io`
- `mne.surface`


## Step-by-Step Guide

### Step 1: 'Test interpolation of EEG field onto head.'

```python
'Test interpolation of EEG field onto head.'
```

**Verification:**
```python
assert len(fmd) == 1
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(evoked_fname, condition='Left Auditory')
```

**Verification:**
```python
assert_array_equal(fmd[0]['data'].shape, (642, 59))
```

### Step 3: Assign unknown = value

```python
evoked.info['bads'] = ['MEG 2443', 'EEG 053']
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 59
```

### Step 4: Assign surf = get_head_surf(...)

```python
surf = get_head_surf('sample', subjects_dir=subjects_dir)
```

### Step 5: Call pytest.raises()

```python
pytest.raises(ValueError, _make_surface_mapping, evoked.info, surf, 'eeg', origin='auto')
```

### Step 6: Call evoked.pick()

```python
evoked.pick(picks='eeg')
```

### Step 7: Assign fmd = make_field_map(...)

```python
fmd = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, origin='auto')
```

### Step 8: Call pytest.raises()

```python
pytest.raises(RuntimeError, make_field_map, evoked, None, subject='sample', subjects_dir=subjects_dir, origin='auto')
```

### Step 9: Assign fmd = make_field_map(...)

```python
fmd = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, origin='auto')
```

**Verification:**
```python
assert len(fmd) == 1
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(fmd[0]['data'].shape, (642, 59))
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 59
```


## Complete Example

```python
# Workflow
'Test interpolation of EEG field onto head.'
evoked = read_evokeds(evoked_fname, condition='Left Auditory')
evoked.info['bads'] = ['MEG 2443', 'EEG 053']
surf = get_head_surf('sample', subjects_dir=subjects_dir)
pytest.raises(ValueError, _make_surface_mapping, evoked.info, surf, 'eeg', origin='auto')
evoked.pick(picks='eeg')
fmd = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, origin='auto')
pytest.raises(RuntimeError, make_field_map, evoked, None, subject='sample', subjects_dir=subjects_dir, origin='auto')
fmd = make_field_map(evoked, trans_fname, subject='sample', subjects_dir=subjects_dir, origin='auto')
assert len(fmd) == 1
assert_array_equal(fmd[0]['data'].shape, (642, 59))
assert len(fmd[0]['ch_names']) == 59
```

## Next Steps


---

*Source: test_field_interpolation.py:132 | Complexity: Advanced | Last updated: 2026-05-18*