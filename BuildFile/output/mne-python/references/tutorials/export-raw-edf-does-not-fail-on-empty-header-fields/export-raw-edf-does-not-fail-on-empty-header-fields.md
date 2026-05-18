# How To: Export Raw Edf Does Not Fail On Empty Header Fields

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test writing a Raw instance with empty header fields to EDF.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.export`
- `mne.fixes`
- `mne.io`
- `mne.tests.test_epochs`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test writing a Raw instance with empty header fields to EDF.'

```python
'Test writing a Raw instance with empty header fields to EDF.'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(123456)
```

### Step 3: Assign ch_types = value

```python
ch_types = ['eeg']
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(len(ch_types), sfreq=1000, ch_types=ch_types)
```

### Step 5: Assign unknown = value

```python
info['subject_info'] = {'his_id': '', 'first_name': '', 'middle_name': '', 'last_name': ''}
```

### Step 6: Assign unknown = value

```python
info['device_info'] = {'type': '123'}
```

### Step 7: Assign data = value

```python
data = rng.random(size=(len(ch_types), 1000)) * 1e-05
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 9: Call raw.export()

```python
raw.export(tmp_path / 'test.edf', add_ch_type=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test writing a Raw instance with empty header fields to EDF.'
rng = np.random.RandomState(123456)
ch_types = ['eeg']
info = create_info(len(ch_types), sfreq=1000, ch_types=ch_types)
info['subject_info'] = {'his_id': '', 'first_name': '', 'middle_name': '', 'last_name': ''}
info['device_info'] = {'type': '123'}
data = rng.random(size=(len(ch_types), 1000)) * 1e-05
raw = RawArray(data, info)
raw.export(tmp_path / 'test.edf', add_ch_type=True)
```

## Next Steps


---

*Source: test_export.py:519 | Complexity: Advanced | Last updated: 2026-05-18*