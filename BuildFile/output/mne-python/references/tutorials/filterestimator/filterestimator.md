# How To: Filterestimator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test methods of FilterEstimator.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.decomposition`
- `sklearn.kernel_ridge`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.defaults`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test methods of FilterEstimator.'

```python
'Test methods of FilterEstimator.'
```

**Verification:**
```python
assert X.shape == epochs_data.shape
```

### Step 2: Assign raw = io.read_raw_fif(...)

```python
raw = io.read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_equal(filt.fit(epochs_data, y).transform(epochs_data), X)
```

### Step 3: Assign events = read_events(...)

```python
events = read_events(event_name)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
```

### Step 5: Assign picks = value

```python
picks = picks[1:13:3]
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), preload=True)
```

### Step 7: Assign epochs_data = epochs.get_data(...)

```python
epochs_data = epochs.get_data(copy=False)
```

### Step 8: Assign filt = FilterEstimator(...)

```python
filt = FilterEstimator(epochs.info, l_freq=40, h_freq=80)
```

### Step 9: Assign y = value

```python
y = epochs.events[:, -1]
```

### Step 10: Assign X = filt.fit_transform(...)

```python
X = filt.fit_transform(epochs_data, y)
```

**Verification:**
```python
assert X.shape == epochs_data.shape
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(filt.fit(epochs_data, y).transform(epochs_data), X)
```

### Step 12: Assign filt = FilterEstimator(...)

```python
filt = FilterEstimator(epochs.info, l_freq=None, h_freq=40, filter_length='auto', l_trans_bandwidth='auto', h_trans_bandwidth='auto')
```

### Step 13: Assign y = value

```python
y = epochs.events[:, -1]
```

### Step 14: Assign X = filt.fit_transform(...)

```python
X = filt.fit_transform(epochs_data, y)
```

### Step 15: Assign filt = FilterEstimator(...)

```python
filt = FilterEstimator(epochs.info, l_freq=1, h_freq=1)
```

### Step 16: Assign y = value

```python
y = epochs.events[:, -1]
```

### Step 17: Assign filt = FilterEstimator(...)

```python
filt = FilterEstimator(epochs.info, l_freq=40, h_freq=None, filter_length='auto', l_trans_bandwidth='auto', h_trans_bandwidth='auto')
```

### Step 18: Assign X = filt.fit_transform(...)

```python
X = filt.fit_transform(epochs_data, y)
```

### Step 19: Call pytest.raises()

```python
pytest.raises(ValueError, filt.fit, 'foo', y)
```

### Step 20: Call pytest.raises()

```python
pytest.raises(ValueError, filt.transform, 'foo')
```

### Step 21: Call pytest.raises()

```python
pytest.raises(ValueError, filt.fit_transform, epochs_data, y)
```


## Complete Example

```python
# Workflow
'Test methods of FilterEstimator.'
raw = io.read_raw_fif(raw_fname)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
picks = picks[1:13:3]
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), preload=True)
epochs_data = epochs.get_data(copy=False)
filt = FilterEstimator(epochs.info, l_freq=40, h_freq=80)
y = epochs.events[:, -1]
X = filt.fit_transform(epochs_data, y)
assert X.shape == epochs_data.shape
assert_array_equal(filt.fit(epochs_data, y).transform(epochs_data), X)
filt = FilterEstimator(epochs.info, l_freq=None, h_freq=40, filter_length='auto', l_trans_bandwidth='auto', h_trans_bandwidth='auto')
y = epochs.events[:, -1]
X = filt.fit_transform(epochs_data, y)
filt = FilterEstimator(epochs.info, l_freq=1, h_freq=1)
y = epochs.events[:, -1]
with pytest.warns(RuntimeWarning, match='longer than the signal'):
    pytest.raises(ValueError, filt.fit_transform, epochs_data, y)
filt = FilterEstimator(epochs.info, l_freq=40, h_freq=None, filter_length='auto', l_trans_bandwidth='auto', h_trans_bandwidth='auto')
X = filt.fit_transform(epochs_data, y)
pytest.raises(ValueError, filt.fit, 'foo', y)
pytest.raises(ValueError, filt.transform, 'foo')
```

## Next Steps


---

*Source: test_transformer.py:127 | Complexity: Advanced | Last updated: 2026-05-18*