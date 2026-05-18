# How To: Concatenate Raws Different Subtypes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test concatenating raws with different subtypes.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `os`
- `pathlib`
- `pickle`
- `platform`
- `shutil`
- `contextlib`
- `copy`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test concatenating raws with different subtypes.'

```python
'Test concatenating raws with different subtypes.'
```

**Verification:**
```python
assert isinstance(result, RawArray)
```

### Step 2: Assign sfreq = 100.0

```python
sfreq = 100.0
```

**Verification:**
```python
assert result.preload
```

### Step 3: Assign ch_names = value

```python
ch_names = ['EEG 001', 'EEG 002']
```

**Verification:**
```python
assert result.n_times == 2 * data.shape[1]
```

### Step 4: Assign ch_types = value

```python
ch_types = ['eeg'] * 2
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, sfreq=sfreq, ch_types=ch_types)
```

### Step 6: Assign data = np.random.randn(...)

```python
data = np.random.randn(len(ch_names), 1000)
```

### Step 7: Assign raw_array = RawArray(...)

```python
raw_array = RawArray(data, info)
```

### Step 8: Call raw_array.save()

```python
raw_array.save(tmp_path / 'temp_raw.fif', overwrite=True)
```

### Step 9: Assign raw_fiff = read_raw_fif(...)

```python
raw_fiff = read_raw_fif(tmp_path / 'temp_raw.fif', preload=True)
```

### Step 10: Assign result = concatenate_raws(...)

```python
result = concatenate_raws([raw_fiff, raw_array])
```

**Verification:**
```python
assert isinstance(result, RawArray)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test concatenating raws with different subtypes.'
sfreq = 100.0
ch_names = ['EEG 001', 'EEG 002']
ch_types = ['eeg'] * 2
info = create_info(ch_names=ch_names, sfreq=sfreq, ch_types=ch_types)
data = np.random.randn(len(ch_names), 1000)
raw_array = RawArray(data, info)
raw_array.save(tmp_path / 'temp_raw.fif', overwrite=True)
raw_fiff = read_raw_fif(tmp_path / 'temp_raw.fif', preload=True)
result = concatenate_raws([raw_fiff, raw_array])
assert isinstance(result, RawArray)
assert result.preload
assert result.n_times == 2 * data.shape[1]
```

## Next Steps


---

*Source: test_raw_fiff.py:491 | Complexity: Advanced | Last updated: 2026-05-18*