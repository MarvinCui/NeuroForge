# How To: Nihon Calibration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test handling of calibration factor and range in Nihon Kohden EEG files.

## Prerequisites

**Required Modules:**
- `pytest`
- `numpy.testing`
- `mne.datasets`
- `mne.io`
- `mne.io.nihon`
- `mne.io.nihon.nihon`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test handling of calibration factor and range in Nihon Kohden EEG files.'

```python
'Test handling of calibration factor and range in Nihon Kohden EEG files.'
```

**Verification:**
```python
assert_allclose(M1_info['cal'], Fp1_info['cal'])
```

### Step 2: Assign fname = value

```python
fname = data_path / 'NihonKohden' / 'DA00100E.EEG'
```

**Verification:**
```python
assert_allclose(M2_info['cal'], Fp1_info['cal'])
```

### Step 3: Assign raw = read_raw_nihon(...)

```python
raw = read_raw_nihon(fname, preload=True, encoding='cp936')
```

**Verification:**
```python
assert_allclose(M1_info['range'], Fp1_info['range'])
```

### Step 4: Assign Fp1_idx = raw.ch_names.index(...)

```python
Fp1_idx = raw.ch_names.index('Fp1')
```

**Verification:**
```python
assert_allclose(M2_info['range'], Fp1_info['range'])
```

### Step 5: Assign M1_idx = raw.ch_names.index(...)

```python
M1_idx = raw.ch_names.index('M1')
```

**Verification:**
```python
assert raw.ch_names == raw_edf.ch_names
```

### Step 6: Assign M2_idx = raw.ch_names.index(...)

```python
M2_idx = raw.ch_names.index('M2')
```

**Verification:**
```python
assert raw._data.shape == raw_edf._data.shape
```

### Step 7: Assign Fp1_info = value

```python
Fp1_info = raw.info['chs'][Fp1_idx]
```

**Verification:**
```python
assert raw.info['sfreq'] == raw_edf.info['sfreq']
```

### Step 8: Assign M1_info = value

```python
M1_info = raw.info['chs'][M1_idx]
```

**Verification:**
```python
assert_allclose(raw.get_data(), raw_edf.get_data())
```

### Step 9: Assign M2_info = value

```python
M2_info = raw.info['chs'][M2_idx]
```

### Step 10: Call assert_allclose()

```python
assert_allclose(M1_info['cal'], Fp1_info['cal'])
```

### Step 11: Call assert_allclose()

```python
assert_allclose(M2_info['cal'], Fp1_info['cal'])
```

### Step 12: Call assert_allclose()

```python
assert_allclose(M1_info['range'], Fp1_info['range'])
```

### Step 13: Call assert_allclose()

```python
assert_allclose(M2_info['range'], Fp1_info['range'])
```

### Step 14: Assign fname_edf = value

```python
fname_edf = data_path / 'NihonKohden' / 'DA00100E.EDF'
```

### Step 15: Assign raw_edf = read_raw_edf(...)

```python
raw_edf = read_raw_edf(fname_edf, preload=True)
```

### Step 16: Call raw_edf.drop_channels()

```python
raw_edf.drop_channels(['Events/Markers'])
```

### Step 17: Assign edf_ch_names = value

```python
edf_ch_names = {'EEG Mark1': '$M1', 'EEG Mark2': '$M2'}
```

### Step 18: Call raw_edf.rename_channels()

```python
raw_edf.rename_channels(edf_ch_names)
```

**Verification:**
```python
assert raw.ch_names == raw_edf.ch_names
```

### Step 19: Call assert_allclose()

```python
assert_allclose(raw.get_data(), raw_edf.get_data())
```


## Complete Example

```python
# Workflow
'Test handling of calibration factor and range in Nihon Kohden EEG files.'
fname = data_path / 'NihonKohden' / 'DA00100E.EEG'
raw = read_raw_nihon(fname, preload=True, encoding='cp936')
Fp1_idx = raw.ch_names.index('Fp1')
M1_idx = raw.ch_names.index('M1')
M2_idx = raw.ch_names.index('M2')
Fp1_info = raw.info['chs'][Fp1_idx]
M1_info = raw.info['chs'][M1_idx]
M2_info = raw.info['chs'][M2_idx]
assert_allclose(M1_info['cal'], Fp1_info['cal'])
assert_allclose(M2_info['cal'], Fp1_info['cal'])
assert_allclose(M1_info['range'], Fp1_info['range'])
assert_allclose(M2_info['range'], Fp1_info['range'])
fname_edf = data_path / 'NihonKohden' / 'DA00100E.EDF'
raw_edf = read_raw_edf(fname_edf, preload=True)
raw_edf.drop_channels(['Events/Markers'])
edf_ch_names = {'EEG Mark1': '$M1', 'EEG Mark2': '$M2'}
raw_edf.rename_channels(edf_ch_names)
assert raw.ch_names == raw_edf.ch_names
assert raw._data.shape == raw_edf._data.shape
assert raw.info['sfreq'] == raw_edf.info['sfreq']
assert_allclose(raw.get_data(), raw_edf.get_data())
```

## Next Steps


---

*Source: test_nihon.py:96 | Complexity: Advanced | Last updated: 2026-05-18*