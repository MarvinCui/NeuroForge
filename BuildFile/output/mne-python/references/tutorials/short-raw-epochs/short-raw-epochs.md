# How To: Short Raw Epochs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Get small data.

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.cov`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.io.eeglab.eeglab`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.ica`
- `mne.rank`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Get small data.'

```python
'Get small data.'
```

**Verification:**
```python
assert 'eog' in raw
```

### Step 2: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0, 5).load_data()
```

**Verification:**
```python
assert len(epochs) == 3
```

### Step 3: Assign picks = value

```python
picks = raw.ch_names[::10] + ['EOG 061', 'MEG 1531', 'MEG 1441', 'MEG 0121']
```

### Step 4: Call raw.pick()

```python
raw.pick(list(filter(lambda ch: ch in picks, raw.ch_names)))
```

**Verification:**
```python
assert 'eog' in raw
```

### Step 5: Call raw.del_proj()

```python
raw.del_proj()
```

### Step 6: Call raw.set_annotations()

```python
raw.set_annotations(Annotations([0.5], [0.5], ['BAD']))
```

### Step 7: Call raw.resample()

```python
raw.resample(100)
```

### Step 8: Assign events = make_fixed_length_events(...)

```python
events = make_fixed_length_events(raw)
```

### Step 9: Assign picks = value

```python
picks = pick_types(raw.info, meg=True, eeg=True, eog=False)[:-1]
```

### Step 10: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, tmin, tmax, picks=picks, baseline=(None, 0), preload=True, proj=False)
```

**Verification:**
```python
assert len(epochs) == 3
```

### Step 11: Assign epochs_eog = Epochs(...)

```python
epochs_eog = Epochs(raw, epochs.events, event_id, tmin, tmax, picks=('meg', 'eog'), baseline=(None, 0), preload=True)
```


## Complete Example

```python
# Workflow
'Get small data.'
raw = read_raw_fif(raw_fname).crop(0, 5).load_data()
picks = raw.ch_names[::10] + ['EOG 061', 'MEG 1531', 'MEG 1441', 'MEG 0121']
raw.pick(list(filter(lambda ch: ch in picks, raw.ch_names)))
assert 'eog' in raw
raw.del_proj()
raw.set_annotations(Annotations([0.5], [0.5], ['BAD']))
raw.resample(100)
events = make_fixed_length_events(raw)
picks = pick_types(raw.info, meg=True, eeg=True, eog=False)[:-1]
epochs = Epochs(raw, events, None, tmin, tmax, picks=picks, baseline=(None, 0), preload=True, proj=False)
assert len(epochs) == 3
epochs_eog = Epochs(raw, epochs.events, event_id, tmin, tmax, picks=('meg', 'eog'), baseline=(None, 0), preload=True)
return (raw, epochs, epochs_eog)
```

## Next Steps


---

*Source: test_ica.py:606 | Complexity: Advanced | Last updated: 2026-05-18*