# How To: Make Info

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test some create_info properties.

## Prerequisites

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`


## Step-by-Step Guide

### Step 1: 'Test some create_info properties.'

```python
'Test some create_info properties.'
```

**Verification:**
```python
assert set(info.keys()) == set(RAW_INFO_FIELDS)
```

### Step 2: Assign n_ch = np.longlong(...)

```python
n_ch = np.longlong(1)
```

**Verification:**
```python
assert FIFF.FIFFV_COIL_EEG in coil_types
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(n_ch, 1000.0, 'eeg')
```

**Verification:**
```python
assert_allclose(ch_pos, ch_pos_mon, atol=1e-05)
```

### Step 4: Assign coil_types = value

```python
coil_types = {ch['coil_type'] for ch in info['chs']}
```

**Verification:**
```python
assert FIFF.FIFFV_COIL_EEG in coil_types
```

### Step 5: Call pytest.raises()

```python
pytest.raises(TypeError, create_info, ch_names='Test Ch', sfreq=1000)
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, create_info, ch_names=['Test Ch'], sfreq=-1000)
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types=['eeg', 'eeg'])
```

### Step 8: Call pytest.raises()

```python
pytest.raises(TypeError, create_info, ch_names=[np.array([1])], sfreq=1000)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(KeyError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types=np.array([1]))
```

### Step 10: Call pytest.raises()

```python
pytest.raises(KeyError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types='awesome')
```

### Step 11: Call pytest.raises()

```python
pytest.raises(TypeError, create_info, ['Test Ch'], sfreq=1000, montage=np.array([1]))
```

### Step 12: Assign m = make_standard_montage(...)

```python
m = make_standard_montage('biosemi32')
```

### Step 13: Assign info = create_info(...)

```python
info = create_info(ch_names=m.ch_names, sfreq=1000.0, ch_types='eeg')
```

### Step 14: Call info.set_montage()

```python
info.set_montage(m)
```

### Step 15: Assign ch_pos = value

```python
ch_pos = [ch['loc'][:3] for ch in info['chs']]
```

### Step 16: Assign ch_pos_mon = m._get_ch_pos(...)

```python
ch_pos_mon = m._get_ch_pos()
```

### Step 17: Assign ch_pos_mon = np.array(...)

```python
ch_pos_mon = np.array([ch_pos_mon[ch_name] for ch_name in info['ch_names']])
```

### Step 18: Call assert_allclose()

```python
assert_allclose(ch_pos, ch_pos_mon, atol=1e-05)
```


## Complete Example

```python
# Workflow
'Test some create_info properties.'
n_ch = np.longlong(1)
info = create_info(n_ch, 1000.0, 'eeg')
assert set(info.keys()) == set(RAW_INFO_FIELDS)
coil_types = {ch['coil_type'] for ch in info['chs']}
assert FIFF.FIFFV_COIL_EEG in coil_types
pytest.raises(TypeError, create_info, ch_names='Test Ch', sfreq=1000)
pytest.raises(ValueError, create_info, ch_names=['Test Ch'], sfreq=-1000)
pytest.raises(ValueError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types=['eeg', 'eeg'])
pytest.raises(TypeError, create_info, ch_names=[np.array([1])], sfreq=1000)
pytest.raises(KeyError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types=np.array([1]))
pytest.raises(KeyError, create_info, ch_names=['Test Ch'], sfreq=1000, ch_types='awesome')
pytest.raises(TypeError, create_info, ['Test Ch'], sfreq=1000, montage=np.array([1]))
m = make_standard_montage('biosemi32')
info = create_info(ch_names=m.ch_names, sfreq=1000.0, ch_types='eeg')
info.set_montage(m)
ch_pos = [ch['loc'][:3] for ch in info['chs']]
ch_pos_mon = m._get_ch_pos()
ch_pos_mon = np.array([ch_pos_mon[ch_name] for ch_name in info['ch_names']])
ch_pos_mon += (0.0, 0.0, 0.04014)
assert_allclose(ch_pos, ch_pos_mon, atol=1e-05)
```

## Next Steps


---

*Source: test_meas_info.py:146 | Complexity: Advanced | Last updated: 2026-05-18*