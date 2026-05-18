# How To: Nedf Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading raw NEDF files.

## Prerequisites

**Required Modules:**
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io.nedf`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test reading raw NEDF files.'

```python
'Test reading raw NEDF files.'
```

**Verification:**
```python
assert nsamples == 32538
```

### Step 2: Assign raw = read_raw_nedf(...)

```python
raw = read_raw_nedf(eegfile)
```

**Verification:**
```python
assert len(events) == 4
```

### Step 3: Assign nsamples = len(...)

```python
nsamples = len(raw)
```

**Verification:**
```python
assert_array_equal(events[:, 2], [1, 1, 1, 1])
```

### Step 4: Assign events = find_events(...)

```python
events = find_events(raw, shortest_event=1)
```

**Verification:**
```python
assert raw.info['sfreq'] == 500
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(events[:, 2], [1, 1, 1, 1])
```

**Verification:**
```python
assert_allclose(data_end, 0.0176, atol=0.01)
```

### Step 6: Assign onsets = value

```python
onsets = events[:, 0] / raw.info['sfreq']
```

**Verification:**
```python
assert_allclose(raw.get_data('Fpz', 0, 100).mean(), 0.0185, atol=0.01)
```

### Step 7: Assign data_end = raw.get_data.mean(...)

```python
data_end = raw.get_data('Fp1', nsamples - 100, nsamples).mean()
```

**Verification:**
```python
assert_allclose(onsets, [22.384, 38.238, 49.496, 63.15])
```

### Step 8: Call assert_allclose()

```python
assert_allclose(data_end, 0.0176, atol=0.01)
```

**Verification:**
```python
assert raw.info['meas_date'].year == 2019
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw.get_data('Fpz', 0, 100).mean(), 0.0185, atol=0.01)
```

**Verification:**
```python
assert raw.ch_names[2] == 'AF7'
```

### Step 10: Call assert_allclose()

```python
assert_allclose(onsets, [22.384, 38.238, 49.496, 63.15])
```

**Verification:**
```python
assert ch['kind'] == FIFF.FIFFV_EEG_CH
```

### Step 11: Call _test_raw_reader()

```python
_test_raw_reader(read_raw_nedf, filename=eegfile)
```

**Verification:**
```python
assert ch['unit'] == FIFF.FIFF_UNIT_V
```


## Complete Example

```python
# Workflow
'Test reading raw NEDF files.'
raw = read_raw_nedf(eegfile)
nsamples = len(raw)
assert nsamples == 32538
events = find_events(raw, shortest_event=1)
assert len(events) == 4
assert_array_equal(events[:, 2], [1, 1, 1, 1])
onsets = events[:, 0] / raw.info['sfreq']
assert raw.info['sfreq'] == 500
data_end = raw.get_data('Fp1', nsamples - 100, nsamples).mean()
assert_allclose(data_end, 0.0176, atol=0.01)
assert_allclose(raw.get_data('Fpz', 0, 100).mean(), 0.0185, atol=0.01)
assert_allclose(onsets, [22.384, 38.238, 49.496, 63.15])
assert raw.info['meas_date'].year == 2019
assert raw.ch_names[2] == 'AF7'
for ch in raw.info['chs'][:-1]:
    assert ch['kind'] == FIFF.FIFFV_EEG_CH
    assert ch['unit'] == FIFF.FIFF_UNIT_V
assert raw.info['chs'][-1]['kind'] == FIFF.FIFFV_STIM_CH
assert raw.info['chs'][-1]['unit'] == FIFF.FIFF_UNIT_V
_test_raw_reader(read_raw_nedf, filename=eegfile)
```

## Next Steps


---

*Source: test_nedf.py:100 | Complexity: Advanced | Last updated: 2026-05-18*