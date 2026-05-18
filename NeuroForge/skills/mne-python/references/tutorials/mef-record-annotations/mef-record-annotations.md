# How To: Mef Record Annotations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test record annotation conversion.

## Prerequisites

**Required Modules:**
- `types`
- `numpy`
- `pytest`
- `mne.datasets`
- `mne.io`
- `mne.io.mef._utils`


## Step-by-Step Guide

### Step 1: 'Test record annotation conversion.'

```python
'Test record annotation conversion.'
```

**Verification:**
```python
assert desc[0] == 'SyLg: chan'
```

### Step 2: Assign start_uutc = 1000000

```python
start_uutc = 1000000
```

**Verification:**
```python
assert ch_names[0] == ['CH01']
```

### Step 3: Assign session = SimpleNamespace(...)

```python
session = SimpleNamespace(session_md={'records_info': {'records': [{'type': 'Note', 'time': start_uutc + 2000000, 'text': 'hello'}]}})
```

**Verification:**
```python
assert extras[0]['channel'] == 'CH01'
```

### Step 4: Assign ts_channels = value

```python
ts_channels = {'CH01': {'records_info': {'records': [{'type': 'SyLg', 'time': start_uutc + 1000000, 'text': 'chan'}]}, 'segments': {'seg-000001': {'records_info': {'records': [{'type': 'EDFA', 'time': start_uutc + 3000000, 'text': 'seg', 'duration': 500000}]}}}}}
```

**Verification:**
```python
assert desc[1] == 'Note: hello'
```

### Step 5: Assign unknown = _records_to_annotations(...)

```python
onsets, durations, desc, ch_names, extras = _records_to_annotations(session, ts_channels, start_uutc)
```

**Verification:**
```python
assert ch_names[1] == []
```

### Step 6: Assign order = np.argsort(...)

```python
order = np.argsort(onsets)
```

**Verification:**
```python
assert desc[2] == 'EDFA: seg'
```

### Step 7: Assign desc = value

```python
desc = [desc[ii] for ii in order]
```

**Verification:**
```python
assert ch_names[2] == ['CH01']
```

### Step 8: Assign ch_names = value

```python
ch_names = [ch_names[ii] for ii in order]
```

**Verification:**
```python
assert extras[2]['segment'] == 'seg-000001'
```

### Step 9: Assign extras = value

```python
extras = [extras[ii] for ii in order]
```

**Verification:**
```python
assert durations[2] == pytest.approx(0.5)
```

### Step 10: Assign durations = value

```python
durations = [durations[ii] for ii in order]
```

**Verification:**
```python
assert desc[0] == 'SyLg: chan'
```


## Complete Example

```python
# Workflow
'Test record annotation conversion.'
start_uutc = 1000000
session = SimpleNamespace(session_md={'records_info': {'records': [{'type': 'Note', 'time': start_uutc + 2000000, 'text': 'hello'}]}})
ts_channels = {'CH01': {'records_info': {'records': [{'type': 'SyLg', 'time': start_uutc + 1000000, 'text': 'chan'}]}, 'segments': {'seg-000001': {'records_info': {'records': [{'type': 'EDFA', 'time': start_uutc + 3000000, 'text': 'seg', 'duration': 500000}]}}}}}
onsets, durations, desc, ch_names, extras = _records_to_annotations(session, ts_channels, start_uutc)
order = np.argsort(onsets)
desc = [desc[ii] for ii in order]
ch_names = [ch_names[ii] for ii in order]
extras = [extras[ii] for ii in order]
durations = [durations[ii] for ii in order]
assert desc[0] == 'SyLg: chan'
assert ch_names[0] == ['CH01']
assert extras[0]['channel'] == 'CH01'
assert desc[1] == 'Note: hello'
assert ch_names[1] == []
assert desc[2] == 'EDFA: seg'
assert ch_names[2] == ['CH01']
assert extras[2]['segment'] == 'seg-000001'
assert durations[2] == pytest.approx(0.5)
```

## Next Steps


---

*Source: test_mef.py:98 | Complexity: Advanced | Last updated: 2026-05-18*