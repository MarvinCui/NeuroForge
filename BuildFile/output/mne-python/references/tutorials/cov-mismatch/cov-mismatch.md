# How To: Cov Mismatch

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test estimation with MEG<->Head mismatch.

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`


## Step-by-Step Guide

### Step 1: 'Test estimation with MEG<->Head mismatch.'

```python
'Test estimation with MEG<->Head mismatch.'
```

### Step 2: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0, 5).load_data()
```

### Step 3: Assign events = find_events(...)

```python
events = find_events(raw, stim_channel='STI 014')
```

### Step 4: Call raw.pick()

```python
raw.pick(raw.ch_names[:5])
```

### Step 5: Call raw.add_proj()

```python
raw.add_proj([], remove_existing=True)
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, tmin=-0.2, tmax=0.0, preload=True)
```

### Step 7: Assign unknown = None

```python
epochs.info['dev_head_t'] = None
```

### Step 8: Assign unknown = None

```python
epochs_2.info['dev_head_t'] = None
```

### Step 9: Call compute_covariance()

```python
compute_covariance([epochs, epochs_2], method=None)
```

### Step 10: Assign epochs_2 = epochs.copy(...)

```python
epochs_2 = epochs.copy()
```

### Step 11: Call compute_covariance()

```python
compute_covariance([epochs, epochs_2])
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, compute_covariance, [epochs, epochs_2])
```

### Step 13: Call compute_covariance()

```python
compute_covariance([epochs, epochs_2], on_mismatch='ignore')
```

### Step 14: Assign unknown = None

```python
epochs_2.info['dev_head_t'] = None
```

### Step 15: Call compute_covariance()

```python
compute_covariance([epochs, epochs_2], on_mismatch='warn')
```

### Step 16: Call compute_covariance()

```python
compute_covariance(epochs, on_mismatch='x')
```


## Complete Example

```python
# Workflow
'Test estimation with MEG<->Head mismatch.'
raw = read_raw_fif(raw_fname).crop(0, 5).load_data()
events = find_events(raw, stim_channel='STI 014')
raw.pick(raw.ch_names[:5])
raw.add_proj([], remove_existing=True)
epochs = Epochs(raw, events, None, tmin=-0.2, tmax=0.0, preload=True)
for kind in ('shift', 'None'):
    epochs_2 = epochs.copy()
    compute_covariance([epochs, epochs_2])
    if kind == 'shift':
        epochs_2.info['dev_head_t']['trans'][:3, 3] += 0.001
    else:
        epochs_2.info['dev_head_t'] = None
    pytest.raises(ValueError, compute_covariance, [epochs, epochs_2])
    compute_covariance([epochs, epochs_2], on_mismatch='ignore')
    with pytest.warns(RuntimeWarning, match='transform mismatch'):
        compute_covariance([epochs, epochs_2], on_mismatch='warn')
    with pytest.raises(ValueError, match='Invalid value'):
        compute_covariance(epochs, on_mismatch='x')
epochs.info['dev_head_t'] = None
epochs_2.info['dev_head_t'] = None
compute_covariance([epochs, epochs_2], method=None)
```

## Next Steps


---

*Source: test_cov.py:142 | Complexity: Advanced | Last updated: 2026-05-18*