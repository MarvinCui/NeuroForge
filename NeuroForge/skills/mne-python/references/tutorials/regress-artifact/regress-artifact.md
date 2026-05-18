# How To: Regress Artifact

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test regressing artifact data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`


## Step-by-Step Guide

### Step 1: 'Test regressing artifact data.'

```python
'Test regressing artifact data.'
```

**Verification:**
```python
assert_allclose(epochs_clean.get_data(copy=False), epochs.get_data(copy=False))
```

### Step 2: Assign raw = read_raw_fif.pick(...)

```python
raw = read_raw_fif(raw_fname).pick(['eeg', 'eog'])
```

**Verification:**
```python
assert orig_norm / 2 > clean_norm > orig_norm / 10
```

### Step 3: Call raw.load_data()

```python
raw.load_data()
```

**Verification:**
```python
assert np.ptp(epochs.get_data('eog')) < 1e-15
```

### Step 4: Assign epochs = create_eog_epochs(...)

```python
epochs = create_eog_epochs(raw)
```

**Verification:**
```python
assert_allclose(betas, 1)
```

### Step 5: Call epochs.apply_baseline()

```python
epochs.apply_baseline((None, None))
```

### Step 6: Assign orig_data = epochs.get_data(...)

```python
orig_data = epochs.get_data('eeg')
```

### Step 7: Assign orig_norm = np.linalg.norm(...)

```python
orig_norm = np.linalg.norm(orig_data)
```

### Step 8: Assign unknown = regress_artifact(...)

```python
epochs_clean, betas = regress_artifact(epochs)
```

### Step 9: Call regress_artifact()

```python
regress_artifact(epochs, betas=betas, copy=False)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(epochs_clean.get_data(copy=False), epochs.get_data(copy=False))
```

### Step 11: Assign clean_data = epochs_clean.get_data(...)

```python
clean_data = epochs_clean.get_data('eeg')
```

### Step 12: Assign clean_norm = np.linalg.norm(...)

```python
clean_norm = np.linalg.norm(clean_data)
```

**Verification:**
```python
assert orig_norm / 2 > clean_norm > orig_norm / 10
```

### Step 13: Assign unknown = regress_artifact(...)

```python
epochs, betas = regress_artifact(epochs, picks='eog', picks_artifact='eog')
```

**Verification:**
```python
assert np.ptp(epochs.get_data('eog')) < 1e-15
```

### Step 14: Call assert_allclose()

```python
assert_allclose(betas, 1)
```

### Step 15: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0, 1).load_data()
```

### Step 16: Call raw.del_proj()

```python
raw.del_proj()
```

### Step 17: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

### Step 18: Assign model = EOGRegression(...)

```python
model = EOGRegression(proj=False, picks='meg', picks_artifact='eog')
```

### Step 19: Call model.fit()

```python
model.fit(raw)
```

### Step 20: Call model.apply()

```python
model.apply(raw)
```

### Step 21: Assign model = EOGRegression(...)

```python
model = EOGRegression(proj=False, picks='eeg', picks_artifact='eog')
```

### Step 22: Call raw.del_proj()

```python
raw.del_proj()
```

### Step 23: Call regress_artifact()

```python
regress_artifact(epochs, betas=betas[:-1])
```

### Step 24: Call model.fit()

```python
model.fit(raw)
```

### Step 25: Call model.fit()

```python
model.fit(raw)
```


## Complete Example

```python
# Workflow
'Test regressing artifact data.'
raw = read_raw_fif(raw_fname).pick(['eeg', 'eog'])
raw.load_data()
epochs = create_eog_epochs(raw)
epochs.apply_baseline((None, None))
orig_data = epochs.get_data('eeg')
orig_norm = np.linalg.norm(orig_data)
epochs_clean, betas = regress_artifact(epochs)
regress_artifact(epochs, betas=betas, copy=False)
assert_allclose(epochs_clean.get_data(copy=False), epochs.get_data(copy=False))
clean_data = epochs_clean.get_data('eeg')
clean_norm = np.linalg.norm(clean_data)
assert orig_norm / 2 > clean_norm > orig_norm / 10
with pytest.raises(ValueError, match='Invalid value.*betas\\.shape.*'):
    regress_artifact(epochs, betas=betas[:-1])
epochs, betas = regress_artifact(epochs, picks='eog', picks_artifact='eog')
assert np.ptp(epochs.get_data('eog')) < 1e-15
assert_allclose(betas, 1)
raw = read_raw_fif(raw_fname).crop(0, 1).load_data()
raw.del_proj()
raw.set_eeg_reference(projection=True)
model = EOGRegression(proj=False, picks='meg', picks_artifact='eog')
model.fit(raw)
model.apply(raw)
model = EOGRegression(proj=False, picks='eeg', picks_artifact='eog')
with pytest.raises(RuntimeError, match='Projections need to be applied'):
    model.fit(raw)
raw.del_proj()
with pytest.raises(RuntimeError, match='No average reference for the EEG'):
    model.fit(raw)
```

## Next Steps


---

*Source: test_regress.py:24 | Complexity: Advanced | Last updated: 2026-05-18*