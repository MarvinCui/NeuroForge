# How To: Ica Reset

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test ICA resetting.

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

### Step 1: 'Test ICA resetting.'

```python
'Test ICA resetting.'
```

**Verification:**
```python
assert ica.current_fit == 'unfitted'
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert all((hasattr(ica, attr) for attr in run_time_attrs))
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
```

**Verification:**
```python
assert ica.labels_ is not None
```

### Step 4: Assign picks = value

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:10]
```

**Verification:**
```python
assert ica.current_fit == 'raw'
```

### Step 5: Assign run_time_attrs = value

```python
run_time_attrs = ('pre_whitener_', 'unmixing_matrix_', 'mixing_matrix_', 'n_components_', 'n_samples_', 'pca_components_', 'pca_explained_variance_', 'pca_mean_', 'n_iter_')
```

**Verification:**
```python
assert not any((hasattr(ica, attr) for attr in run_time_attrs))
```

### Step 6: Assign ica = ICA(...)

```python
ica = ICA(n_components=3, method=method, max_iter=1)
```

**Verification:**
```python
assert ica.labels_ is not None
```

### Step 7: Call ica._reset()

```python
ica._reset()
```

**Verification:**
```python
assert ica.current_fit == 'unfitted'
```

### Step 8: Call ica.fit()

```python
ica.fit(raw, picks=picks)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test ICA resetting.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:10]
run_time_attrs = ('pre_whitener_', 'unmixing_matrix_', 'mixing_matrix_', 'n_components_', 'n_samples_', 'pca_components_', 'pca_explained_variance_', 'pca_mean_', 'n_iter_')
ica = ICA(n_components=3, method=method, max_iter=1)
assert ica.current_fit == 'unfitted'
with pytest.warns(UserWarning, match='did not converge'):
    ica.fit(raw, picks=picks)
assert all((hasattr(ica, attr) for attr in run_time_attrs))
assert ica.labels_ is not None
assert ica.current_fit == 'raw'
ica._reset()
assert not any((hasattr(ica, attr) for attr in run_time_attrs))
assert ica.labels_ is not None
assert ica.current_fit == 'unfitted'
```

## Next Steps


---

*Source: test_ica.py:427 | Complexity: Advanced | Last updated: 2026-05-18*