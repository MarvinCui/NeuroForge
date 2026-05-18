# How To: Get Inst Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _get_inst_data.

## Prerequisites

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: 'Test _get_inst_data.'

```python
'Test _get_inst_data.'
```

**Verification:**
```python
assert_array_equal(_get_inst_data(raw), raw._data)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw)
```

**Verification:**
```python
assert_array_equal(_get_inst_data(epochs), epochs._data)
```

### Step 3: Call raw.crop()

```python
raw.crop(tmax=1.0)
```

**Verification:**
```python
assert_array_equal(_get_inst_data(evoked), evoked.data)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(_get_inst_data(raw), raw._data)
```

**Verification:**
```python
assert_array_equal(_get_inst_data(tfr), tfr.data)
```

### Step 5: Call raw.pick()

```python
raw.pick(raw.ch_names[:2])
```

### Step 6: Assign epochs = make_fixed_length_epochs(...)

```python
epochs = make_fixed_length_epochs(raw, 0.5)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(_get_inst_data(epochs), epochs._data)
```

### Step 8: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(_get_inst_data(evoked), evoked.data)
```

### Step 10: Call evoked.crop()

```python
evoked.crop(tmax=0.1)
```

### Step 11: Assign picks = list(...)

```python
picks = list(range(2))
```

### Step 12: Assign freqs = value

```python
freqs = [50.0, 55.0]
```

### Step 13: Assign n_cycles = 3

```python
n_cycles = 3
```

### Step 14: Assign tfr = tfr_morlet(...)

```python
tfr = tfr_morlet(evoked, freqs, n_cycles, return_itc=False, picks=picks)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(_get_inst_data(tfr), tfr.data)
```

### Step 16: Call pytest.raises()

```python
pytest.raises(TypeError, _get_inst_data, 'foo')
```


## Complete Example

```python
# Workflow
'Test _get_inst_data.'
raw = read_raw_fif(fname_raw)
raw.crop(tmax=1.0)
assert_array_equal(_get_inst_data(raw), raw._data)
raw.pick(raw.ch_names[:2])
epochs = make_fixed_length_epochs(raw, 0.5)
assert_array_equal(_get_inst_data(epochs), epochs._data)
evoked = epochs.average()
assert_array_equal(_get_inst_data(evoked), evoked.data)
evoked.crop(tmax=0.1)
picks = list(range(2))
freqs = [50.0, 55.0]
n_cycles = 3
tfr = tfr_morlet(evoked, freqs, n_cycles, return_itc=False, picks=picks)
assert_array_equal(_get_inst_data(tfr), tfr.data)
pytest.raises(TypeError, _get_inst_data, 'foo')
```

## Next Steps


---

*Source: test_numerics.py:55 | Complexity: Advanced | Last updated: 2026-05-18*