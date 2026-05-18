# How To: Ica Reject Buffer

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test ICA data raw buffer rejection.

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

### Step 1: 'Test ICA data raw buffer rejection.'

```python
'Test ICA data raw buffer rejection.'
```

**Verification:**
```python
assert raw._data[:5, ::2].shape[1] - 4 == ica.n_samples_
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert_equal(len(log), 1)
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
```

### Step 5: Assign unknown = 5e-12

```python
raw._data[2, 1000:1005] = 5e-12
```

### Step 6: Assign ica = ICA(...)

```python
ica = ICA(n_components=3, method=method)
```

### Step 7: Assign log = value

```python
log = [line for line in drop_log.getvalue().split('\n') if 'detected' in line]
```

### Step 8: Call assert_equal()

```python
assert_equal(len(log), 1)
```

### Step 9: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

### Step 10: Call ica.fit()

```python
ica.fit(raw, picks[:5], reject=dict(mag=2.5e-12), decim=2, tstep=0.01, verbose=True, reject_by_annotation=False)
```

**Verification:**
```python
assert raw._data[:5, ::2].shape[1] - 4 == ica.n_samples_
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test ICA data raw buffer rejection.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
raw._data[2, 1000:1005] = 5e-12
ica = ICA(n_components=3, method=method)
with catch_logging() as drop_log:
    ica.fit(raw, picks[:5], reject=dict(mag=2.5e-12), decim=2, tstep=0.01, verbose=True, reject_by_annotation=False)
    assert raw._data[:5, ::2].shape[1] - 4 == ica.n_samples_
log = [line for line in drop_log.getvalue().split('\n') if 'detected' in line]
assert_equal(len(log), 1)
_assert_ica_attributes(ica)
```

## Next Steps


---

*Source: test_ica.py:1160 | Complexity: Advanced | Last updated: 2026-05-18*