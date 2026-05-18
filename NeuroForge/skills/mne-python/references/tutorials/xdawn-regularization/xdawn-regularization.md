# How To: Xdawn Regularization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Xdawn with regularization.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.io`
- `mne.decoding.xdawn`
- `mne.preprocessing.xdawn`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `mne.decoding`


## Step-by-Step Guide

### Step 1: 'Test Xdawn with regularization.'

```python
'Test Xdawn with regularization.'
```

**Verification:**
```python
assert xd.correct_overlap_
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert np.sum(np.abs(evoked.data - xd.evokeds_['cond2'].data))
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, verbose=False, preload=True)
```

### Step 4: Assign events = read_events(...)

```python
events = read_events(event_name)
```

### Step 5: Assign picks = value

```python
picks = pick_types(raw.info, meg=True, eeg=False, stim=False, ecg=False, eog=False, exclude='bads')[::8]
```

### Step 6: Call raw.pick()

```python
raw.pick([raw.ch_names[pick] for pick in picks])
```

### Step 7: Call raw.info.normalize_proj()

```python
raw.info.normalize_proj()
```

### Step 8: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, preload=True, baseline=None, verbose=False)
```

### Step 9: Assign events = value

```python
events = epochs.events
```

### Step 10: Assign sel = value

```python
sel = np.where(events[:, 2] == 2)[0][:2]
```

### Step 11: Assign modified_event = value

```python
modified_event = events[sel[0]]
```

### Step 12: Assign unknown = modified_event

```python
epochs.events[sel[1]] = modified_event
```

### Step 13: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap='auto', reg='oas')
```

### Step 14: Call xd.fit()

```python
xd.fit(epochs)
```

**Verification:**
```python
assert xd.correct_overlap_
```

### Step 15: Assign evoked = unknown.average(...)

```python
evoked = epochs['cond2'].average()
```

**Verification:**
```python
assert np.sum(np.abs(evoked.data - xd.evokeds_['cond2'].data))
```

### Step 16: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=np.eye(len(epochs.ch_names)), reg=2)
```

### Step 17: Assign xd = Xdawn(...)

```python
xd = Xdawn(correct_overlap=False, reg=0.5)
```

### Step 18: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 19: Assign xd = Xdawn(...)

```python
xd = Xdawn(correct_overlap=False, reg='diagonal_fixed')
```

### Step 20: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 21: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=np.eye(len(epochs.ch_names)), reg=reg)
```

### Step 22: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 23: Call xd.fit()

```python
xd.fit(epochs)
```


## Complete Example

```python
# Workflow
'Test Xdawn with regularization.'
pytest.importorskip('sklearn')
raw = read_raw_fif(raw_fname, verbose=False, preload=True)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, eeg=False, stim=False, ecg=False, eog=False, exclude='bads')[::8]
raw.pick([raw.ch_names[pick] for pick in picks])
del picks
raw.info.normalize_proj()
epochs = Epochs(raw, events, event_id, tmin, tmax, preload=True, baseline=None, verbose=False)
events = epochs.events
sel = np.where(events[:, 2] == 2)[0][:2]
modified_event = events[sel[0]]
modified_event[0] += 1
epochs.events[sel[1]] = modified_event
xd = Xdawn(n_components=2, correct_overlap='auto', reg='oas')
xd.fit(epochs)
assert xd.correct_overlap_
evoked = epochs['cond2'].average()
assert np.sum(np.abs(evoked.data - xd.evokeds_['cond2'].data))
for reg in [0.1, 0.1, 'ledoit_wolf', 'oas']:
    xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=np.eye(len(epochs.ch_names)), reg=reg)
    xd.fit(epochs)
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=np.eye(len(epochs.ch_names)), reg=2)
with pytest.raises(ValueError, match='shrinkage must be'):
    xd.fit(epochs)
xd = Xdawn(correct_overlap=False, reg=0.5)
xd.fit(epochs)
xd = Xdawn(correct_overlap=False, reg='diagonal_fixed')
xd.fit(epochs)
```

## Next Steps


---

*Source: test_xdawn.py:178 | Complexity: Advanced | Last updated: 2026-05-18*