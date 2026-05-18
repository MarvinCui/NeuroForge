# How To: Eog Channel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that EOG channel is included when performing ICA.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: 'Test that EOG channel is included when performing ICA.'

```python
'Test that EOG channel is included when performing ICA.'
```

**Verification:**
```python
assert any(('EOG' in ch for ch in ica.ch_names))
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert not any(('EOG' in ch for ch in ica.ch_names))
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

### Step 4: Assign events = read_events(...)

```python
events = read_events(event_name)
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, stim=True, ecg=False, eog=True, exclude='bads')
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=None, preload=True, proj=False)
```

### Step 7: Assign n_components = 0.9

```python
n_components = 0.9
```

### Step 8: Assign ica = ICA(...)

```python
ica = ICA(n_components=n_components, method=method)
```

### Step 9: Assign picks1a = value

```python
picks1a = pick_types(inst.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:4]
```

### Step 10: Assign picks1b = pick_types(...)

```python
picks1b = pick_types(inst.info, meg=False, stim=False, ecg=False, eog=True, exclude='bads')
```

### Step 11: Assign picks1 = np.append(...)

```python
picks1 = np.append(picks1a, picks1b)
```

### Step 12: Call ica.fit()

```python
ica.fit(inst, picks=picks1)
```

**Verification:**
```python
assert any(('EOG' in ch for ch in ica.ch_names))
```

### Step 13: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica, inst.get_data(picks1), limits=(0.8, 600))
```

### Step 14: Assign picks1 = value

```python
picks1 = pick_types(inst.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:5]
```

### Step 15: Call ica.fit()

```python
ica.fit(inst, picks=picks1)
```

### Step 16: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

**Verification:**
```python
assert not any(('EOG' in ch for ch in ica.ch_names))
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test that EOG channel is included when performing ICA.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname, preload=True)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, stim=True, ecg=False, eog=True, exclude='bads')
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=None, preload=True, proj=False)
n_components = 0.9
ica = ICA(n_components=n_components, method=method)
for inst in [raw, epochs]:
    picks1a = pick_types(inst.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:4]
    picks1b = pick_types(inst.info, meg=False, stim=False, ecg=False, eog=True, exclude='bads')
    picks1 = np.append(picks1a, picks1b)
    ica.fit(inst, picks=picks1)
    assert any(('EOG' in ch for ch in ica.ch_names))
    _assert_ica_attributes(ica, inst.get_data(picks1), limits=(0.8, 600))
for inst in [raw, epochs]:
    picks1 = pick_types(inst.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:5]
    ica.fit(inst, picks=picks1)
    _assert_ica_attributes(ica)
    assert not any(('EOG' in ch for ch in ica.ch_names))
```

## Next Steps


---

*Source: test_ica.py:1333 | Complexity: Advanced | Last updated: 2026-05-18*