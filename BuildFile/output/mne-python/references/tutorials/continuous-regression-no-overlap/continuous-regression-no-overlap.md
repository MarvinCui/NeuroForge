# How To: Continuous Regression No Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test regression without overlap correction, on real data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal.windows`
- `mne`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.stats.regression`
- `sklearn.linear_model`


## Step-by-Step Guide

### Step 1: 'Test regression without overlap correction, on real data.'

```python
'Test regression without overlap correction, on real data.'
```

**Verification:**
```python
assert_allclose(revokeds[cond].data, epochs[cond].average().data, rtol=1e-15)
```

### Step 2: Assign unknown = value

```python
tmin, tmax = (-0.1, 0.5)
```

### Step 3: Assign raw = mne.io.read_raw_fif(...)

```python
raw = mne.io.read_raw_fif(raw_fname, preload=True)
```

### Step 4: Call raw.apply_proj()

```python
raw.apply_proj()
```

### Step 5: Assign events = mne.read_events(...)

```python
events = mne.read_events(event_fname)
```

### Step 6: Assign event_id = dict(...)

```python
event_id = dict(audio_l=1, audio_r=2)
```

### Step 7: Assign raw = raw.pick(...)

```python
raw = raw.pick(raw.ch_names[:2])
```

### Step 8: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, baseline=None, reject=None)
```

### Step 9: Assign revokeds = linear_regression_raw(...)

```python
revokeds = linear_regression_raw(raw, events, event_id, tmin=tmin, tmax=tmax, reject=None)
```

### Step 10: Assign old_latency = value

```python
old_latency = events[1, 0]
```

### Step 11: Assign unknown = value

```python
events[1, 0] = events[0, 0]
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, linear_regression_raw, raw, events, event_id, tmin, tmax)
```

### Step 13: Assign unknown = old_latency

```python
events[1, 0] = old_latency
```

### Step 14: Assign unknown = range(...)

```python
events[:, 0] = range(len(events))
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, linear_regression_raw, raw, events, event_id, tmin, tmax, decim=2)
```

### Step 16: Assign unknown = 128

```python
raw.info['sfreq'] = 128
```

### Step 17: Call assert_allclose()

```python
assert_allclose(revokeds[cond].data, epochs[cond].average().data, rtol=1e-15)
```


## Complete Example

```python
# Workflow
'Test regression without overlap correction, on real data.'
tmin, tmax = (-0.1, 0.5)
raw = mne.io.read_raw_fif(raw_fname, preload=True)
raw.apply_proj()
with raw.info._unlock():
    raw.info['sfreq'] = 128
events = mne.read_events(event_fname)
event_id = dict(audio_l=1, audio_r=2)
raw = raw.pick(raw.ch_names[:2])
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, baseline=None, reject=None)
revokeds = linear_regression_raw(raw, events, event_id, tmin=tmin, tmax=tmax, reject=None)
for cond in event_id.keys():
    assert_allclose(revokeds[cond].data, epochs[cond].average().data, rtol=1e-15)
old_latency = events[1, 0]
events[1, 0] = events[0, 0]
pytest.raises(ValueError, linear_regression_raw, raw, events, event_id, tmin, tmax)
events[1, 0] = old_latency
events[:, 0] = range(len(events))
pytest.raises(ValueError, linear_regression_raw, raw, events, event_id, tmin, tmax, decim=2)
```

## Next Steps


---

*Source: test_regression.py:80 | Complexity: Advanced | Last updated: 2026-05-18*