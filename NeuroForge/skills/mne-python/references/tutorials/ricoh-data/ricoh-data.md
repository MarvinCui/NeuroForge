# How To: Ricoh Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading channel names and dig information from Ricoh systems.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, fname, desc
```

## Step-by-Step Guide

### Step 1: 'Test reading channel names and dig information from Ricoh systems.'

```python
'Test reading channel names and dig information from Ricoh systems.'
```

**Verification:**
```python
assert raw.ch_names[0] == 'MEG 001'
```

### Step 2: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(fname, standardize_names=True)
```

**Verification:**
```python
assert raw.info['description'] == desc
```

### Step 3: Assign raw = read_raw_kit(...)

```python
raw = read_raw_kit(fname, standardize_names=False, verbose='debug')
```

**Verification:**
```python
assert_allclose(raw.times[-1], 5.0 - 1.0 / raw.info['sfreq'])
```

### Step 4: Call assert_allclose()

```python
assert_allclose(raw.times[-1], 5.0 - 1.0 / raw.info['sfreq'])
```

**Verification:**
```python
assert raw.ch_names[0] == 'LF31'
```

### Step 5: Assign eeg_picks = pick_types(...)

```python
eeg_picks = pick_types(raw.info, meg=False, eeg=True)
```

**Verification:**
```python
assert len(eeg_picks) == 45
```

### Step 6: Assign bad_dig = value

```python
bad_dig = [ch['ch_name'] for ci, ch in enumerate(raw.info['chs']) if ci in eeg_picks and (ch['loc'][:3] == 0).all()]
```

**Verification:**
```python
assert len(raw.info['dig']) == 8 + len(eeg_picks) - 2
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw.info['dev_head_t']['trans'], [[0.998311, -0.056923, 0.01164, 0.001403], [0.054469, 0.986653, 0.153458, 0.0044], [-0.02022, -0.152564, 0.988087, 0.018634], [0.0, 0.0, 0.0, 1.0]], atol=1e-05)
```

**Verification:**
```python
assert bad_dig == ['EKG+', 'E']
```

### Step 8: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert not any((np.allclose(d['r'], 0.0) for d in raw.info['dig']))
```

### Step 9: Call _assert_sinusoid()

```python
_assert_sinusoid(data[0], raw.times, 10, 1e-12, '1 pT 10 Hz MEG')
```

**Verification:**
```python
assert_allclose(raw.info['dev_head_t']['trans'], [[0.998311, -0.056923, 0.01164, 0.001403], [0.054469, 0.986653, 0.153458, 0.0044], [-0.02022, -0.152564, 0.988087, 0.018634], [0.0, 0.0, 0.0, 1.0]], atol=1e-05)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(data[1:160], 0.0, atol=1e-13)
```

**Verification:**
```python
assert raw.info['chs'][0]['coil_type'] == FIFF.FIFFV_COIL_KIT_GRAD
```

### Step 11: Call _assert_sinusoid()

```python
_assert_sinusoid(data[160], raw.times, 5, 1, '1 V 5 Hz analog')
```

**Verification:**
```python
assert_allclose(data[1:160], 0.0, atol=1e-13)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(data[161:185], 0.0, atol=1e-20)
```

**Verification:**
```python
assert raw.info['chs'][186]['coil_type'] == FIFF.FIFFV_COIL_EEG
```

### Step 13: Assign eeg_data = value

```python
eeg_data = data[186]
```

**Verification:**
```python
assert_allclose(data[161:185], 0.0, atol=1e-20)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(eeg_data.mean(), 0.0016, atol=1e-05)
```

**Verification:**
```python
assert raw.info['chs'][186]['coil_type'] == FIFF.FIFFV_COIL_EEG
```

### Step 15: Assign eeg_data = value

```python
eeg_data = eeg_data - eeg_data.mean()
```

**Verification:**
```python
assert_allclose(eeg_data.mean(), 0.0016, atol=1e-05)
```

### Step 16: Call _assert_sinusoid()

```python
_assert_sinusoid(eeg_data, raw.times, 8, 5e-05, '50 uV 8 Hz EEG')
```

**Verification:**
```python
assert_allclose(data[187:-1], 0.0, atol=1e-20)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(data[187:-1], 0.0, atol=1e-20)
```

**Verification:**
```python
assert_allclose(data[-1], 254.5, atol=0.51)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(data[-1], 254.5, atol=0.51)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname, desc

# Workflow
'Test reading channel names and dig information from Ricoh systems.'
raw = read_raw_kit(fname, standardize_names=True)
assert raw.ch_names[0] == 'MEG 001'
raw = read_raw_kit(fname, standardize_names=False, verbose='debug')
assert raw.info['description'] == desc
assert_allclose(raw.times[-1], 5.0 - 1.0 / raw.info['sfreq'])
assert raw.ch_names[0] == 'LF31'
eeg_picks = pick_types(raw.info, meg=False, eeg=True)
assert len(eeg_picks) == 45
assert len(raw.info['dig']) == 8 + len(eeg_picks) - 2
bad_dig = [ch['ch_name'] for ci, ch in enumerate(raw.info['chs']) if ci in eeg_picks and (ch['loc'][:3] == 0).all()]
assert bad_dig == ['EKG+', 'E']
assert not any((np.allclose(d['r'], 0.0) for d in raw.info['dig']))
assert_allclose(raw.info['dev_head_t']['trans'], [[0.998311, -0.056923, 0.01164, 0.001403], [0.054469, 0.986653, 0.153458, 0.0044], [-0.02022, -0.152564, 0.988087, 0.018634], [0.0, 0.0, 0.0, 1.0]], atol=1e-05)
data = raw.get_data()
assert raw.info['chs'][0]['coil_type'] == FIFF.FIFFV_COIL_KIT_GRAD
_assert_sinusoid(data[0], raw.times, 10, 1e-12, '1 pT 10 Hz MEG')
assert_allclose(data[1:160], 0.0, atol=1e-13)
assert raw.info['chs'][186]['coil_type'] == FIFF.FIFFV_COIL_EEG
_assert_sinusoid(data[160], raw.times, 5, 1, '1 V 5 Hz analog')
assert_allclose(data[161:185], 0.0, atol=1e-20)
assert raw.info['chs'][186]['coil_type'] == FIFF.FIFFV_COIL_EEG
eeg_data = data[186]
assert_allclose(eeg_data.mean(), 0.0016, atol=1e-05)
eeg_data = eeg_data - eeg_data.mean()
_assert_sinusoid(eeg_data, raw.times, 8, 5e-05, '50 uV 8 Hz EEG')
assert_allclose(data[187:-1], 0.0, atol=1e-20)
assert_allclose(data[-1], 254.5, atol=0.51)
```

## Next Steps


---

*Source: test_kit.py:237 | Complexity: Advanced | Last updated: 2026-05-18*