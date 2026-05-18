# How To: N Components None

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test n_components=None.

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
# Fixtures: method, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test n_components=None.'

```python
'Test n_components=None.'
```

**Verification:**
```python
assert ica.n_pca_components is None
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert ica.n_components is None
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
```

**Verification:**
```python
assert ica.n_components_ == len(picks)
```

### Step 4: Assign events = read_events(...)

```python
events = read_events(event_name)
```

### Step 5: Assign picks = value

```python
picks = pick_types(raw.info, eeg=True, meg=False)[::5]
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), preload=True)
```

### Step 7: Assign n_components = None

```python
n_components = None
```

### Step 8: Assign random_state = 12345

```python
random_state = 12345
```

### Step 9: Assign output_fname = value

```python
output_fname = tmp_path / 'test_ica-ica.fif'
```

### Step 10: Assign ica = ICA(...)

```python
ica = ICA(method=method, n_components=n_components, random_state=random_state)
```

### Step 11: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

### Step 12: Call ica.save()

```python
ica.save(output_fname)
```

### Step 13: Assign ica = read_ica(...)

```python
ica = read_ica(output_fname)
```

### Step 14: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

**Verification:**
```python
assert ica.n_pca_components is None
```

### Step 15: Call ica.fit()

```python
ica.fit(epochs)
```


## Complete Example

```python
# Setup
# Fixtures: method, tmp_path

# Workflow
'Test n_components=None.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
events = read_events(event_name)
picks = pick_types(raw.info, eeg=True, meg=False)[::5]
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), preload=True)
n_components = None
random_state = 12345
output_fname = tmp_path / 'test_ica-ica.fif'
ica = ICA(method=method, n_components=n_components, random_state=random_state)
with _record_warnings():
    ica.fit(epochs)
_assert_ica_attributes(ica)
ica.save(output_fname)
ica = read_ica(output_fname)
_assert_ica_attributes(ica)
assert ica.n_pca_components is None
assert ica.n_components is None
assert ica.n_components_ == len(picks)
```

## Next Steps


---

*Source: test_ica.py:1377 | Complexity: Advanced | Last updated: 2026-05-18*