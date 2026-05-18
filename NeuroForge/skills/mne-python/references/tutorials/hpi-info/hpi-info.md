# How To: Hpi Info

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test getting HPI info.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test getting HPI info.'

```python
'Test getting HPI info.'
```

**Verification:**
```python
assert len(raw.info['hpi_subsystem']) > 0
```

### Step 2: Assign temp_name = value

```python
temp_name = tmp_path / 'temp_raw.fif'
```

**Verification:**
```python
assert len(info['hpi_subsystem']) == len(raw.info['hpi_subsystem'])
```

### Step 3: Assign info = read_info(...)

```python
info = read_info(chpi_fif_fname)
```

**Verification:**
```python
assert_allclose(hpi_freqs, np.array([83.0, 143.0, 203.0, 263.0, 323.0]))
```

### Step 4: Assign unknown = get_chpi_info(...)

```python
hpi_freqs, stim_ch_idx, hpi_on_codes = get_chpi_info(info)
```

**Verification:**
```python
assert stim_ch_idx == 378
```

### Step 5: Call assert_allclose()

```python
assert_allclose(hpi_freqs, np.array([83.0, 143.0, 203.0, 263.0, 323.0]))
```

**Verification:**
```python
assert_allclose(hpi_on_codes, np.array([256, 512, 1024, 2048, 4096]))
```

### Step 6: Call assert_allclose()

```python
assert_allclose(hpi_on_codes, np.array([256, 512, 1024, 2048, 4096]))
```

**Verification:**
```python
assert_array_equal([], hpi_freqs)
```

### Step 7: Assign unknown = get_chpi_info(...)

```python
hpi_freqs, stim_ch_idx, hpi_on_codes = get_chpi_info(info, on_missing='ignore')
```

**Verification:**
```python
assert stim_ch_idx is None
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal([], hpi_freqs)
```

**Verification:**
```python
assert_array_equal([], hpi_on_codes)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal([], hpi_on_codes)
```

### Step 10: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(fname, allow_maxshield='yes').crop(0, 0.1)
```

**Verification:**
```python
assert len(raw.info['hpi_subsystem']) > 0
```

### Step 11: Call raw.save()

```python
raw.save(temp_name, overwrite=True)
```

### Step 12: Assign info = read_info(...)

```python
info = read_info(temp_name)
```

**Verification:**
```python
assert len(info['hpi_subsystem']) == len(raw.info['hpi_subsystem'])
```

### Step 13: Assign unknown = None

```python
info['hpi_subsystem'] = None
```

### Step 14: Assign unknown = value

```python
info['hpi_meas'] = []
```

### Step 15: Assign unknown = value

```python
info['hpi_results'] = []
```

### Step 16: Call get_chpi_info()

```python
get_chpi_info(info)
```

### Step 17: Call get_chpi_info()

```python
get_chpi_info(info, on_missing='warn')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test getting HPI info.'
temp_name = tmp_path / 'temp_raw.fif'
for fname in (chpi_fif_fname, sss_fif_fname):
    raw = read_raw_fif(fname, allow_maxshield='yes').crop(0, 0.1)
    assert len(raw.info['hpi_subsystem']) > 0
    raw.save(temp_name, overwrite=True)
    info = read_info(temp_name)
    assert len(info['hpi_subsystem']) == len(raw.info['hpi_subsystem'])
info = read_info(chpi_fif_fname)
hpi_freqs, stim_ch_idx, hpi_on_codes = get_chpi_info(info)
assert_allclose(hpi_freqs, np.array([83.0, 143.0, 203.0, 263.0, 323.0]))
assert stim_ch_idx == 378
assert_allclose(hpi_on_codes, np.array([256, 512, 1024, 2048, 4096]))
with info._unlock():
    info['hpi_subsystem'] = None
    info['hpi_meas'] = []
    info['hpi_results'] = []
with pytest.raises(ValueError, match='No appropriate cHPI information'):
    get_chpi_info(info)
with pytest.warns(RuntimeWarning, match='No appropriate cHPI information'):
    get_chpi_info(info, on_missing='warn')
hpi_freqs, stim_ch_idx, hpi_on_codes = get_chpi_info(info, on_missing='ignore')
assert_array_equal([], hpi_freqs)
assert stim_ch_idx is None
assert_array_equal([], hpi_on_codes)
```

## Next Steps


---

*Source: test_chpi.py:163 | Complexity: Advanced | Last updated: 2026-05-18*