# How To: Ica Twice

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test running ICA twice.

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

### Step 1: 'Test running ICA twice.'

```python
'Test running ICA twice.'
```

**Verification:**
```python
assert_equal(ica1.n_components_, ica2.n_components_)
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
```

### Step 4: Call raw.pick()

```python
raw.pick(raw.ch_names[::10])
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg='grad', exclude='bads')
```

### Step 6: Assign n_components = 0.99

```python
n_components = 0.99
```

### Step 7: Assign n_pca_components = 0.9999

```python
n_pca_components = 0.9999
```

### Step 8: Assign ica1 = ICA(...)

```python
ica1 = ICA(n_components=n_components, method=method)
```

### Step 9: Assign raw_new = ica1.apply(...)

```python
raw_new = ica1.apply(raw, n_pca_components=n_pca_components)
```

### Step 10: Assign ica2 = ICA(...)

```python
ica2 = ICA(n_components=n_components, method=method)
```

### Step 11: Call assert_equal()

```python
assert_equal(ica1.n_components_, ica2.n_components_)
```

### Step 12: Assign ctx = _record_warnings

```python
ctx = _record_warnings
```

### Step 13: Assign ctx = nullcontext

```python
ctx = nullcontext
```

### Step 14: Call ica1.fit()

```python
ica1.fit(raw, picks=picks, decim=3)
```

### Step 15: Call ica2.fit()

```python
ica2.fit(raw_new, picks=picks, decim=3)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test running ICA twice.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(1.5, stop).load_data()
raw.pick(raw.ch_names[::10])
picks = pick_types(raw.info, meg='grad', exclude='bads')
n_components = 0.99
n_pca_components = 0.9999
if method == 'fastica':
    ctx = _record_warnings
else:
    ctx = nullcontext
ica1 = ICA(n_components=n_components, method=method)
with ctx():
    ica1.fit(raw, picks=picks, decim=3)
raw_new = ica1.apply(raw, n_pca_components=n_pca_components)
ica2 = ICA(n_components=n_components, method=method)
with ctx():
    ica2.fit(raw_new, picks=picks, decim=3)
assert_equal(ica1.n_components_, ica2.n_components_)
```

## Next Steps


---

*Source: test_ica.py:1186 | Complexity: Advanced | Last updated: 2026-05-18*