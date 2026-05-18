# How To: Estimate Montage Units

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test automatic estimation of montage units.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `time`
- `copy`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.annotations`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.io.eeglab._eeglab`
- `mne.io.eeglab.eeglab`
- `mne.io.tests.test_raw`
- `mne.utils`
- `eeglabio.raw`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test automatic estimation of montage units.'

```python
'Test automatic estimation of montage units.'
```

**Verification:**
```python
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_m.info['chs']]))
```

### Step 2: Assign m_fname = value

```python
m_fname = tmp_path / 'test_montage_m.set'
```

**Verification:**
```python
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_cm.info['chs']]))
```

### Step 3: Call _create_eeg_with_scaled_montage_units()

```python
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, m_fname, 0.001)
```

### Step 4: Assign cm_fname = value

```python
cm_fname = tmp_path / 'test_montage_cm.set'
```

### Step 5: Call _create_eeg_with_scaled_montage_units()

```python
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, cm_fname, 0.1)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_m.info['chs']]))
```

### Step 7: Call assert_allclose()

```python
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_cm.info['chs']]))
```

### Step 8: Assign raw_mm = read_raw_eeglab(...)

```python
raw_mm = read_raw_eeglab(raw_fname_chanloc, montage_units='auto')
```

### Step 9: Assign raw_m = read_raw_eeglab(...)

```python
raw_m = read_raw_eeglab(m_fname, montage_units='auto')
```

### Step 10: Assign raw_cm = read_raw_eeglab(...)

```python
raw_cm = read_raw_eeglab(cm_fname, montage_units='auto')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test automatic estimation of montage units.'
m_fname = tmp_path / 'test_montage_m.set'
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, m_fname, 0.001)
cm_fname = tmp_path / 'test_montage_cm.set'
_create_eeg_with_scaled_montage_units(raw_fname_chanloc, cm_fname, 0.1)
with pytest.warns(RuntimeWarning, match="The data contains 'boundary' events"):
    raw_mm = read_raw_eeglab(raw_fname_chanloc, montage_units='auto')
    raw_m = read_raw_eeglab(m_fname, montage_units='auto')
    raw_cm = read_raw_eeglab(cm_fname, montage_units='auto')
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_m.info['chs']]))
assert_allclose(np.array([ch['loc'] for ch in raw_mm.info['chs']]), np.array([ch['loc'] for ch in raw_cm.info['chs']]))
```

## Next Steps


---

*Source: test_eeglab.py:637 | Complexity: Advanced | Last updated: 2026-05-18*