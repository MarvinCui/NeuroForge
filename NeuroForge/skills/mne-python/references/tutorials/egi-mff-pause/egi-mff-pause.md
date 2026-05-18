# How To: Egi Mff Pause

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test EGI MFF with pauses.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.egi.egi`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, skip_times, event_times
```

## Step-by-Step Guide

### Step 1: 'Test EGI MFF with pauses.'

```python
'Test EGI MFF with pauses.'
```

**Verification:**
```python
assert raw.info['sfreq'] == 250.0
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert raw.info['dev_head_t'] is None
```

### Step 3: Assign stim_picks = pick_types(...)

```python
stim_picks = pick_types(raw.info, meg=False, stim=True, exclude=())
```

**Verification:**
```python
assert len(raw.annotations) == len(skip_times)
```

### Step 4: Assign other_picks = np.setdiff1d(...)

```python
other_picks = np.setdiff1d(np.arange(len(raw.ch_names)), stim_picks)
```

**Verification:**
```python
assert_array_equal(events[events[:, 2] == raw.event_id[event_type], 0], ns_samples)
```

### Step 5: Assign raw = read_raw_egi.load_data(...)

```python
raw = read_raw_egi(fname, events_as_annotations=False).load_data()
```

**Verification:**
```python
assert annot['description'] == 'BAD_ACQ_SKIP'
```

### Step 6: Assign events = find_events(...)

```python
events = find_events(raw)
```

**Verification:**
```python
assert_array_equal(data[other_picks], 0.0)
```

### Step 7: Assign unknown = raw.time_as_index(...)

```python
start, stop = raw.time_as_index([annot['onset'], annot['onset'] + annot['duration']])
```

**Verification:**
```python
assert raw.ch_names[-1] == 'STI 014'
```

### Step 8: Assign unknown = value

```python
data, _ = raw[:, start:stop]
```

**Verification:**
```python
assert not np.array_equal(data[stim_picks], 0.0)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data[other_picks], 0.0)
```

**Verification:**
```python
assert skip == skip_times[ii]
```

### Step 10: Assign skip = value

```python
skip = ((start + 1) / raw.info['sfreq'] * 1000000.0, (stop + 1) / raw.info['sfreq'] * 1000000.0)
```

**Verification:**
```python
assert skip == skip_times[ii]
```

### Step 11: Assign raw = _test_raw_reader(...)

```python
raw = _test_raw_reader(read_raw_egi, input_fname=fname, test_scaling=False, test_rank='less', events_as_annotations=False)
```

### Step 12: Call find_events()

```python
find_events(raw)
```

### Step 13: Assign ns_samples = np.floor(...)

```python
ns_samples = np.floor(np.array(event_times[event_type]) * raw.info['sfreq'])
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(events[events[:, 2] == raw.event_id[event_type], 0], ns_samples)
```

**Verification:**
```python
assert raw.ch_names[-1] == 'STI 014'
```


## Complete Example

```python
# Setup
# Fixtures: fname, skip_times, event_times

# Workflow
'Test EGI MFF with pauses.'
pytest.importorskip('defusedxml')
if fname == egi_pause_w1337_fname:
    raw = read_raw_egi(fname, events_as_annotations=False).load_data()
else:
    with pytest.warns(RuntimeWarning, match='Acquisition skips detected'):
        raw = _test_raw_reader(read_raw_egi, input_fname=fname, test_scaling=False, test_rank='less', events_as_annotations=False)
assert raw.info['sfreq'] == 250.0
assert raw.info['dev_head_t'] is None
assert len(raw.annotations) == len(skip_times)
if event_times is None:
    with pytest.raises(ValueError, match='Consider using .*events_from'):
        find_events(raw)
else:
    events = find_events(raw)
    for event_type in event_times.keys():
        ns_samples = np.floor(np.array(event_times[event_type]) * raw.info['sfreq'])
        assert_array_equal(events[events[:, 2] == raw.event_id[event_type], 0], ns_samples)
stim_picks = pick_types(raw.info, meg=False, stim=True, exclude=())
other_picks = np.setdiff1d(np.arange(len(raw.ch_names)), stim_picks)
for ii, annot in enumerate(raw.annotations):
    assert annot['description'] == 'BAD_ACQ_SKIP'
    start, stop = raw.time_as_index([annot['onset'], annot['onset'] + annot['duration']])
    data, _ = raw[:, start:stop]
    assert_array_equal(data[other_picks], 0.0)
    if event_times is not None:
        assert raw.ch_names[-1] == 'STI 014'
        assert not np.array_equal(data[stim_picks], 0.0)
    skip = ((start + 1) / raw.info['sfreq'] * 1000000.0, (stop + 1) / raw.info['sfreq'] * 1000000.0)
    assert skip == skip_times[ii]
```

## Next Steps


---

*Source: test_egi.py:69 | Complexity: Advanced | Last updated: 2026-05-18*