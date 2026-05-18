# How To: Spectrum Io

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test save/load of spectrum objects.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: inst, tmp_path, request, evoked
```

## Step-by-Step Guide

### Step 1: 'Test save/load of spectrum objects.'

```python
'Test save/load of spectrum objects.'
```

**Verification:**
```python
assert orig == loaded
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('h5io')
```

**Verification:**
```python
assert isinstance(loaded.info['subject_info']['birthday'], datetime.date)
```

### Step 3: Assign h5py = pytest.importorskip(...)

```python
h5py = pytest.importorskip('h5py')
```

**Verification:**
```python
assert origavg == loadedavg
```

### Step 4: Assign fname = value

```python
fname = tmp_path / f'{inst}-spectrum.h5'
```

### Step 5: Assign inst = _get_inst(...)

```python
inst = _get_inst(inst, request, evoked=evoked)
```

### Step 6: Assign orig = inst.compute_psd(...)

```python
orig = inst.compute_psd()
```

### Step 7: Call orig.save()

```python
orig.save(fname)
```

### Step 8: Assign loaded = read_spectrum(...)

```python
loaded = read_spectrum(fname)
```

**Verification:**
```python
assert orig == loaded
```

### Step 9: Assign fname_subject_info = value

```python
fname_subject_info = tmp_path / 'subject-info.h5'
```

### Step 10: Assign unknown = _import_h5io_funcs(...)

```python
_, write_hdf5 = _import_h5io_funcs()
```

### Step 11: Call write_hdf5()

```python
write_hdf5(fname_subject_info, dict(birthday=(2000, 1, 1)), title='subject_info')
```

### Step 12: Assign loaded = read_spectrum(...)

```python
loaded = read_spectrum(fname)
```

**Verification:**
```python
assert isinstance(loaded.info['subject_info']['birthday'], datetime.date)
```

### Step 13: Assign origavg = orig.average(...)

```python
origavg = orig.average()
```

### Step 14: Call origavg.save()

```python
origavg.save(fname, overwrite=True)
```

### Step 15: Assign loadedavg = read_spectrum(...)

```python
loadedavg = read_spectrum(fname)
```

**Verification:**
```python
assert origavg == loadedavg
```

### Step 16: Assign unknown = 2

```python
inst.events[-2:, -1] = 2
```

### Step 17: Assign inst.event_id = value

```python
inst.event_id = {'foo/bar': 1, 'foo/qux': 2}
```

### Step 18: Assign orig = value

```python
orig = orig['foo']
```

### Step 19: Assign unknown = h5py.ExternalLink(...)

```python
f['mnepython/key_info/key_subject_info'] = h5py.ExternalLink(fname_subject_info, 'subject_info')
```


## Complete Example

```python
# Setup
# Fixtures: inst, tmp_path, request, evoked

# Workflow
'Test save/load of spectrum objects.'
pytest.importorskip('h5io')
h5py = pytest.importorskip('h5py')
fname = tmp_path / f'{inst}-spectrum.h5'
inst = _get_inst(inst, request, evoked=evoked)
if isinstance(inst, BaseEpochs):
    inst.events[-2:, -1] = 2
    inst.event_id = {'foo/bar': 1, 'foo/qux': 2}
orig = inst.compute_psd()
if isinstance(inst, BaseEpochs):
    orig = orig['foo']
orig.save(fname)
loaded = read_spectrum(fname)
assert orig == loaded
if not isinstance(inst, BaseEpochs):
    return
fname_subject_info = tmp_path / 'subject-info.h5'
_, write_hdf5 = _import_h5io_funcs()
write_hdf5(fname_subject_info, dict(birthday=(2000, 1, 1)), title='subject_info')
with h5py.File(fname, 'r+') as f:
    del f['mnepython/key_info/key_subject_info']
    f['mnepython/key_info/key_subject_info'] = h5py.ExternalLink(fname_subject_info, 'subject_info')
loaded = read_spectrum(fname)
assert isinstance(loaded.info['subject_info']['birthday'], datetime.date)
origavg = orig.average()
origavg.save(fname, overwrite=True)
loadedavg = read_spectrum(fname)
assert origavg == loadedavg
```

## Next Steps


---

*Source: test_spectrum.py:179 | Complexity: Advanced | Last updated: 2026-05-18*