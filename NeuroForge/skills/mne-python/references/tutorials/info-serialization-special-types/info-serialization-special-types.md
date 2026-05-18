# How To: Info Serialization Special Types

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that special types (NamedInt, dates, etc.) are preserved correctly.

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

### Step 1: 'Test that special types (NamedInt, dates, etc.) are preserved correctly.'

```python
'Test that special types (NamedInt, dates, etc.) are preserved correctly.'
```

**Verification:**
```python
assert isinstance(info_restored['meas_date'], datetime)
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(ch_names=['EEG1'], sfreq=1000.0, ch_types='eeg')
```

**Verification:**
```python
assert info_restored['meas_date'] == meas_date
```

### Step 3: Assign meas_date = datetime(...)

```python
meas_date = datetime(2023, 11, 13, 10, 30, 0, tzinfo=timezone.utc)
```

**Verification:**
```python
assert isinstance(info_restored['subject_info']['birthday'], date)
```

### Step 4: Assign unknown = value

```python
info['subject_info'] = {'id': 1, 'his_id': 'SUBJ001', 'birthday': date(1990, 1, 15), 'sex': 1}
```

**Verification:**
```python
assert info_restored['subject_info']['birthday'] == date(1990, 1, 15)
```

### Step 5: Assign info_dict = info.to_json_dict(...)

```python
info_dict = info.to_json_dict()
```

**Verification:**
```python
assert isinstance(info_restored['custom_ref_applied'], NamedInt)
```

### Step 6: Assign json_str = json.dumps(...)

```python
json_str = json.dumps(info_dict)
```

**Verification:**
```python
assert repr(info['custom_ref_applied']) == repr(info_restored['custom_ref_applied'])
```

### Step 7: Assign info_restored = Info.from_json_dict(...)

```python
info_restored = Info.from_json_dict(json.loads(json_str))
```

**Verification:**
```python
assert isinstance(info_restored['meas_date'], datetime)
```

### Step 8: Assign unknown = meas_date

```python
info['meas_date'] = meas_date
```


## Complete Example

```python
# Workflow
'Test that special types (NamedInt, dates, etc.) are preserved correctly.'
from mne.utils._bunch import NamedInt
info = create_info(ch_names=['EEG1'], sfreq=1000.0, ch_types='eeg')
meas_date = datetime(2023, 11, 13, 10, 30, 0, tzinfo=timezone.utc)
with info._unlock():
    info['meas_date'] = meas_date
info['subject_info'] = {'id': 1, 'his_id': 'SUBJ001', 'birthday': date(1990, 1, 15), 'sex': 1}
info_dict = info.to_json_dict()
json_str = json.dumps(info_dict)
info_restored = Info.from_json_dict(json.loads(json_str))
assert isinstance(info_restored['meas_date'], datetime)
assert info_restored['meas_date'] == meas_date
assert isinstance(info_restored['subject_info']['birthday'], date)
assert info_restored['subject_info']['birthday'] == date(1990, 1, 15)
assert isinstance(info_restored['custom_ref_applied'], NamedInt)
assert repr(info['custom_ref_applied']) == repr(info_restored['custom_ref_applied'])
```

## Next Steps


---

*Source: test_meas_info.py:399 | Complexity: Advanced | Last updated: 2026-05-18*