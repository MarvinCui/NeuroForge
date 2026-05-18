# How To: Ica Rank Reduction

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test recovery ICA rank reduction.

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

### Step 1: 'Test recovery ICA rank reduction.'

```python
'Test recovery ICA rank reduction.'
```

**Verification:**
```python
assert_equal(rank_before, len(picks))
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert n_components < n_pca_components <= rank_after <= rank_before
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
```

### Step 4: Assign picks = value

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:10]
```

### Step 5: Assign n_components = 5

```python
n_components = 5
```

### Step 6: Assign rank_before = _compute_rank_int(...)

```python
rank_before = _compute_rank_int(raw.copy().pick(picks), proj=False)
```

### Step 7: Call assert_equal()

```python
assert_equal(rank_before, len(picks))
```

### Step 8: Assign raw_clean = ica.apply(...)

```python
raw_clean = ica.apply(raw.copy(), n_pca_components=n_pca_components)
```

### Step 9: Assign rank_after = _compute_rank_int(...)

```python
rank_after = _compute_rank_int(raw_clean.copy().pick(picks), proj=False)
```

**Verification:**
```python
assert n_components < n_pca_components <= rank_after <= rank_before
```

### Step 10: Assign ica = ICA.fit(...)

```python
ica = ICA(n_components=n_components, method=method, max_iter=1).fit(raw, picks=picks)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test recovery ICA rank reduction.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')[:10]
n_components = 5
for n_pca_components in [6, 10]:
    with pytest.warns(UserWarning, match='did not converge'):
        ica = ICA(n_components=n_components, method=method, max_iter=1).fit(raw, picks=picks)
    rank_before = _compute_rank_int(raw.copy().pick(picks), proj=False)
    assert_equal(rank_before, len(picks))
    raw_clean = ica.apply(raw.copy(), n_pca_components=n_pca_components)
    rank_after = _compute_rank_int(raw_clean.copy().pick(picks), proj=False)
    assert n_components < n_pca_components <= rank_after <= rank_before
```

## Next Steps


---

*Source: test_ica.py:326 | Complexity: Advanced | Last updated: 2026-05-18*