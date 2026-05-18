# How To: Eximia Nxe

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading Eximia NXE files.

## Prerequisites

**Required Modules:**
- `numpy.testing`
- `scipy`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test reading Eximia NXE files.'

```python
'Test reading Eximia NXE files.'
```

**Verification:**
```python
assert 'RawEximia' in repr(raw)
```

### Step 2: Assign fname = value

```python
fname = testing_path / 'eximia' / 'test_eximia.nxe'
```

**Verification:**
```python
assert raw._data.shape == m_data.shape
```

### Step 3: Assign raw = read_raw_eximia(...)

```python
raw = read_raw_eximia(fname, preload=True)
```

**Verification:**
```python
assert m_header['Fs'][0, 0][0, 0] == raw.info['sfreq']
```

### Step 4: Call _test_raw_reader()

```python
_test_raw_reader(read_raw_eximia, fname=fname, test_scaling=False)
```

**Verification:**
```python
assert raw.ch_names == m_names
```

### Step 5: Assign fname_mat = value

```python
fname_mat = testing_path / 'eximia' / 'test_eximia.mat'
```

**Verification:**
```python
assert ch_types == m_ch_types
```

### Step 6: Assign mc = sio.loadmat(...)

```python
mc = sio.loadmat(fname_mat)
```

**Verification:**
```python
assert_array_equal(m_data, raw._data)
```

### Step 7: Assign m_data = value

```python
m_data = mc['data']
```

### Step 8: Assign m_header = value

```python
m_header = mc['header']
```

**Verification:**
```python
assert raw._data.shape == m_data.shape
```

### Step 9: Assign m_names = value

```python
m_names = [x[0][0] for x in m_header['label'][0, 0]]
```

### Step 10: Assign m_names = list(...)

```python
m_names = list(map(lambda x: x.replace('GATE', 'GateIn').replace('TRIG', 'Trig'), m_names))
```

**Verification:**
```python
assert raw.ch_names == m_names
```

### Step 11: Assign m_ch_types = value

```python
m_ch_types = [x[0][0] for x in m_header['chantype'][0, 0]]
```

### Step 12: Assign m_ch_types = list(...)

```python
m_ch_types = list(map(lambda x: x.replace('unknown', 'stim').replace('trigger', 'stim'), m_ch_types))
```

### Step 13: Assign types_dict = value

```python
types_dict = {2: 'eeg', 3: 'stim', 202: 'eog'}
```

### Step 14: Assign ch_types = value

```python
ch_types = [types_dict[raw.info['chs'][x]['kind']] for x in range(len(raw.ch_names))]
```

**Verification:**
```python
assert ch_types == m_ch_types
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(m_data, raw._data)
```


## Complete Example

```python
# Workflow
'Test reading Eximia NXE files.'
fname = testing_path / 'eximia' / 'test_eximia.nxe'
raw = read_raw_eximia(fname, preload=True)
assert 'RawEximia' in repr(raw)
_test_raw_reader(read_raw_eximia, fname=fname, test_scaling=False)
fname_mat = testing_path / 'eximia' / 'test_eximia.mat'
mc = sio.loadmat(fname_mat)
m_data = mc['data']
m_header = mc['header']
assert raw._data.shape == m_data.shape
assert m_header['Fs'][0, 0][0, 0] == raw.info['sfreq']
m_names = [x[0][0] for x in m_header['label'][0, 0]]
m_names = list(map(lambda x: x.replace('GATE', 'GateIn').replace('TRIG', 'Trig'), m_names))
assert raw.ch_names == m_names
m_ch_types = [x[0][0] for x in m_header['chantype'][0, 0]]
m_ch_types = list(map(lambda x: x.replace('unknown', 'stim').replace('trigger', 'stim'), m_ch_types))
types_dict = {2: 'eeg', 3: 'stim', 202: 'eog'}
ch_types = [types_dict[raw.info['chs'][x]['kind']] for x in range(len(raw.ch_names))]
assert ch_types == m_ch_types
assert_array_equal(m_data, raw._data)
```

## Next Steps


---

*Source: test_eximia.py:16 | Complexity: Advanced | Last updated: 2026-05-18*