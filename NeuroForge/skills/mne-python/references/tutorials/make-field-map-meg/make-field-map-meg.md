# How To: Make Field Map Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interpolation of MEG field onto helmet | head.

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

### Step 1: 'Test interpolation of MEG field onto helmet | head.'

```python
'Test interpolation of MEG field onto helmet | head.'
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
assert_array_equal(fmd[0]['data'].shape, (304, 106))
```

### Step 3: Assign info = value

```python
info = evoked.info
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 106
```

### Step 4: Assign surf = get_meg_helmet_surf(...)

```python
surf = get_meg_helmet_surf(info)
```

**Verification:**
```python
assert len(fmd) == 1
```

### Step 5: Assign unknown = value

```python
info['bads'] = info['ch_names'][:200]
```

**Verification:**
```python
assert_array_equal(fmd[0]['data'].shape, (642, 106))
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, _make_surface_mapping, info, surf, 'foo', origin='auto')
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 106
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, _make_surface_mapping, info, surf, 'meg', mode='foo', origin='auto')
```

### Step 8: Assign evoked_eeg = evoked.copy.pick(...)

```python
evoked_eeg = evoked.copy().pick(picks='eeg')
```

### Step 9: Call pytest.raises()

```python
pytest.raises(RuntimeError, _make_surface_mapping, evoked_eeg.info, surf, 'meg', origin='auto')
```

### Step 10: Assign nn = value

```python
nn = surf['nn']
```

### Step 11: Call pytest.raises()

```python
pytest.raises(KeyError, _make_surface_mapping, info, surf, 'meg', origin='auto')
```

### Step 12: Assign unknown = nn

```python
surf['nn'] = nn
```

### Step 13: Assign cf = value

```python
cf = surf['coord_frame']
```

### Step 14: Call pytest.raises()

```python
pytest.raises(KeyError, _make_surface_mapping, info, surf, 'meg', origin='auto')
```

### Step 15: Assign unknown = cf

```python
surf['coord_frame'] = cf
```

### Step 16: Call evoked.pick()

```python
evoked.pick(picks='meg')
```

### Step 17: Call evoked.info.normalize_proj()

```python
evoked.info.normalize_proj()
```

### Step 18: Assign fmd = make_field_map(...)

```python
fmd = make_field_map(evoked, None, subject='sample', subjects_dir=subjects_dir, origin='auto')
```

**Verification:**
```python
assert len(fmd) == 1
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(fmd[0]['data'].shape, (304, 106))
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 106
```

### Step 20: Call pytest.raises()

```python
pytest.raises(ValueError, make_field_map, evoked, ch_type='foobar', origin='auto')
```

### Step 21: Call evoked.pick()

```python
evoked.pick(picks='meg')
```

### Step 22: Call evoked.info.normalize_proj()

```python
evoked.info.normalize_proj()
```

### Step 23: Assign fmd = make_field_map(...)

```python
fmd = make_field_map(evoked, trans_fname, meg_surf='head', subject='sample', subjects_dir=subjects_dir, origin='auto')
```

**Verification:**
```python
assert len(fmd) == 1
```

### Step 24: Call assert_array_equal()

```python
assert_array_equal(fmd[0]['data'].shape, (642, 106))
```

**Verification:**
```python
assert len(fmd[0]['ch_names']) == 106
```

### Step 25: Call pytest.raises()

```python
pytest.raises(ValueError, make_field_map, evoked, meg_surf='foobar', subjects_dir=subjects_dir, trans=trans_fname, origin='auto')
```


## Complete Example

```python
# Workflow
'Test interpolation of MEG field onto helmet | head.'
evoked = read_evokeds(evoked_fname, condition='Left Auditory')
info = evoked.info
surf = get_meg_helmet_surf(info)
info['bads'] = info['ch_names'][:200]
pytest.raises(ValueError, _make_surface_mapping, info, surf, 'foo', origin='auto')
pytest.raises(ValueError, _make_surface_mapping, info, surf, 'meg', mode='foo', origin='auto')
evoked_eeg = evoked.copy().pick(picks='eeg')
pytest.raises(RuntimeError, _make_surface_mapping, evoked_eeg.info, surf, 'meg', origin='auto')
nn = surf['nn']
del surf['nn']
pytest.raises(KeyError, _make_surface_mapping, info, surf, 'meg', origin='auto')
surf['nn'] = nn
cf = surf['coord_frame']
del surf['coord_frame']
pytest.raises(KeyError, _make_surface_mapping, info, surf, 'meg', origin='auto')
surf['coord_frame'] = cf
evoked.pick(picks='meg')
evoked.info.normalize_proj()
fmd = make_field_map(evoked, None, subject='sample', subjects_dir=subjects_dir, origin='auto')
assert len(fmd) == 1
assert_array_equal(fmd[0]['data'].shape, (304, 106))
assert len(fmd[0]['ch_names']) == 106
pytest.raises(ValueError, make_field_map, evoked, ch_type='foobar', origin='auto')
evoked.pick(picks='meg')
evoked.info.normalize_proj()
fmd = make_field_map(evoked, trans_fname, meg_surf='head', subject='sample', subjects_dir=subjects_dir, origin='auto')
assert len(fmd) == 1
assert_array_equal(fmd[0]['data'].shape, (642, 106))
assert len(fmd[0]['ch_names']) == 106
pytest.raises(ValueError, make_field_map, evoked, meg_surf='foobar', subjects_dir=subjects_dir, trans=trans_fname, origin='auto')
```

## Next Steps


---

*Source: test_field_interpolation.py:168 | Complexity: Advanced | Last updated: 2026-05-18*