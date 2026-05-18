# How To: Read Vhdr Annotations And Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test load brainvision annotations and parse them to events.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test load brainvision annotations and parse them to events.'

```python
'Test load brainvision annotations and parse them to events.'
```

**Verification:**
```python
assert raw.annotations.orig_time == expected_orig_time
```

### Step 2: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

**Verification:**
```python
assert_allclose(raw.annotations.onset, expected_onset_latency / sfreq)
```

### Step 3: Assign expected_orig_time = _stamp_to_dt(...)

```python
expected_orig_time = _stamp_to_dt((1384359243, 794232))
```

**Verification:**
```python
assert_array_equal(raw.annotations.description, expected_annot_description)
```

### Step 4: Assign expected_onset_latency = np.array(...)

```python
expected_onset_latency = np.array([486.0, 496.0, 1769.0, 1779.0, 3252.0, 3262.0, 4935.0, 4945.0, 5999.0, 6619.0, 6629.0, 7629.0, 7699.0, 7799.0])
```

**Verification:**
```python
assert_array_equal(events, expected_events)
```

### Step 5: Assign expected_annot_description = value

```python
expected_annot_description = ['Stimulus/S253', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Stimulus/S253', 'Stimulus/S255', 'Response/R255', 'Event/254', 'Stimulus/S255', 'SyncStatus/Sync On', 'Optic/O  1', 'Comma,Type/CommaValue,1']
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 6: Assign expected_events = value

```python
expected_events = np.stack([expected_onset_latency, np.zeros_like(expected_onset_latency), [253, 255, 254, 255, 254, 255, 253, 255, 1255, 254, 255, 99998, 2001, 10001]]).astype('int64').T
```

**Verification:**
```python
assert event_id == expected_none_event_id
```

### Step 7: Assign expected_event_id = value

```python
expected_event_id = {'Stimulus/S253': 253, 'Stimulus/S255': 255, 'Event/254': 254, 'Response/R255': 1255, 'SyncStatus/Sync On': 99998, 'Optic/O  1': 2001, 'Comma,Type/CommaValue,1': 10001}
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 8: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(tmp_path / 'test.vhdr', eog=eog)
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw.annotations.onset, expected_onset_latency / sfreq)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description, expected_annot_description)
```

### Step 11: Assign unknown = events_from_annotations(...)

```python
events, event_id = events_from_annotations(raw)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(events, expected_events)
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 13: Assign expected_none_event_id = value

```python
expected_none_event_id = {desc: idx + 1 for idx, desc in enumerate(sorted(event_id.keys()))}
```

### Step 14: Assign unknown = events_from_annotations(...)

```python
events, event_id = events_from_annotations(raw, event_id=None)
```

**Verification:**
```python
assert event_id == expected_none_event_id
```

### Step 15: Assign s_10 = 'Stimulus/S 10'

```python
s_10 = 'Stimulus/S 10'
```

### Step 16: Call raw.annotations.append()

```python
raw.annotations.append([1, 2, 3], 10, ['ZZZ', s_10, 'YYY'])
```

### Step 17: Call expected_event_id.update()

```python
expected_event_id.update(YYY=10002, ZZZ=10003)
```

### Step 18: Assign unknown = 10

```python
expected_event_id[s_10] = 10
```

### Step 19: Assign unknown = events_from_annotations(...)

```python
_, event_id = events_from_annotations(raw)
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 20: Assign unknown = events_from_annotations(...)

```python
_, event_id = events_from_annotations(raw_concat)
```

**Verification:**
```python
assert event_id == expected_event_id
```

### Step 21: Call shutil.copyfile()

```python
shutil.copyfile(src, tmp_path / dest)
```

### Step 22: Call fout.write()

```python
fout.write('Mk15=Comma\\1Type,CommaValue\\11,7800,1,0\\n')
```

### Step 23: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws([raw.copy(), raw.copy()])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test load brainvision annotations and parse them to events.'
for src, dest in zip((vhdr_path, vmrk_path, eeg_path), ('test.vhdr', 'test.vmrk', 'test.eeg')):
    shutil.copyfile(src, tmp_path / dest)
with open(tmp_path / 'test.vmrk', 'a') as fout:
    fout.write('Mk15=Comma\\1Type,CommaValue\\11,7800,1,0\\n')
sfreq = 1000.0
expected_orig_time = _stamp_to_dt((1384359243, 794232))
expected_onset_latency = np.array([486.0, 496.0, 1769.0, 1779.0, 3252.0, 3262.0, 4935.0, 4945.0, 5999.0, 6619.0, 6629.0, 7629.0, 7699.0, 7799.0])
expected_annot_description = ['Stimulus/S253', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Stimulus/S253', 'Stimulus/S255', 'Response/R255', 'Event/254', 'Stimulus/S255', 'SyncStatus/Sync On', 'Optic/O  1', 'Comma,Type/CommaValue,1']
expected_events = np.stack([expected_onset_latency, np.zeros_like(expected_onset_latency), [253, 255, 254, 255, 254, 255, 253, 255, 1255, 254, 255, 99998, 2001, 10001]]).astype('int64').T
expected_event_id = {'Stimulus/S253': 253, 'Stimulus/S255': 255, 'Event/254': 254, 'Response/R255': 1255, 'SyncStatus/Sync On': 99998, 'Optic/O  1': 2001, 'Comma,Type/CommaValue,1': 10001}
raw = read_raw_brainvision(tmp_path / 'test.vhdr', eog=eog)
assert raw.annotations.orig_time == expected_orig_time
assert_allclose(raw.annotations.onset, expected_onset_latency / sfreq)
assert_array_equal(raw.annotations.description, expected_annot_description)
events, event_id = events_from_annotations(raw)
assert_array_equal(events, expected_events)
assert event_id == expected_event_id
expected_none_event_id = {desc: idx + 1 for idx, desc in enumerate(sorted(event_id.keys()))}
events, event_id = events_from_annotations(raw, event_id=None)
assert event_id == expected_none_event_id
s_10 = 'Stimulus/S 10'
raw.annotations.append([1, 2, 3], 10, ['ZZZ', s_10, 'YYY'])
expected_event_id.update(YYY=10002, ZZZ=10003)
expected_event_id[s_10] = 10
_, event_id = events_from_annotations(raw)
assert event_id == expected_event_id
with pytest.warns(RuntimeWarning, match='expanding outside'):
    raw_concat = concatenate_raws([raw.copy(), raw.copy()])
_, event_id = events_from_annotations(raw_concat)
assert event_id == expected_event_id
```

## Next Steps


---

*Source: test_brainvision.py:903 | Complexity: Advanced | Last updated: 2026-05-18*