# How To: Edf Temperature

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test that we can parse temperature channel type.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test that we can parse temperature channel type.'

```python
'Test that we can parse temperature channel type.'
```

**Verification:**
```python
assert raw.get_channel_types()[0] == 'eeg'
```

### Step 2: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path)
```

**Verification:**
```python
assert 'temperature' in raw
```

### Step 3: Call monkeypatch.setattr()

```python
monkeypatch.setattr(edf.edf, '_read_edf_header', _first_chan_temp)
```

**Verification:**
```python
assert raw.get_channel_types()[0] == 'temperature'
```

### Step 4: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path)
```

**Verification:**
```python
assert 'temperature' in raw
```

### Step 5: Assign unknown = _read_edf_header(...)

```python
out, orig_units = _read_edf_header(*args, **kwargs)
```

### Step 6: Assign unknown = 'TEMP'

```python
out['ch_types'][0] = 'TEMP'
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test that we can parse temperature channel type.'
raw = read_raw_edf(edf_path)
assert raw.get_channel_types()[0] == 'eeg'

def _first_chan_temp(*args, **kwargs):
    out, orig_units = _read_edf_header(*args, **kwargs)
    out['ch_types'][0] = 'TEMP'
    return (out, orig_units)
monkeypatch.setattr(edf.edf, '_read_edf_header', _first_chan_temp)
raw = read_raw_edf(edf_path)
assert 'temperature' in raw
assert raw.get_channel_types()[0] == 'temperature'
```

## Next Steps


---

*Source: test_edf.py:101 | Complexity: Intermediate | Last updated: 2026-05-18*