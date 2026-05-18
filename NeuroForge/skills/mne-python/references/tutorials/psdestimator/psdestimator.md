# How To: Psdestimator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test methods of PSDEstimator.

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

### Step 1: 'Test methods of PSDEstimator.'

```python
'Test methods of PSDEstimator.'
```

**Verification:**
```python
assert not hasattr(psd, 'fitted_')
```

### Step 2: Assign raw = io.read_raw_fif(...)

```python
raw = io.read_raw_fif(raw_fname)
```

**Verification:**
```python
assert psd.fitted_
```

### Step 3: Assign events = read_events(...)

```python
events = read_events(event_name)
```

**Verification:**
```python
assert X.shape[0] == epochs_data.shape[0]
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
```

**Verification:**
```python
assert_array_equal(psd.fit(epochs_data, y).transform(epochs_data), X)
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

### Step 8: Assign psd = PSDEstimator(...)

```python
psd = PSDEstimator(2 * np.pi, 0, np.inf)
```

### Step 9: Assign y = value

```python
y = epochs.events[:, -1]
```

**Verification:**
```python
assert not hasattr(psd, 'fitted_')
```

### Step 10: Assign X = psd.fit_transform(...)

```python
X = psd.fit_transform(epochs_data, y)
```

**Verification:**
```python
assert psd.fitted_
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(psd.fit(epochs_data, y).transform(epochs_data), X)
```

### Step 12: Call psd.fit()

```python
psd.fit('foo', y)
```

### Step 13: Call psd.transform()

```python
psd.transform('foo')
```


## Complete Example

```python
# Workflow
'Test methods of PSDEstimator.'
raw = io.read_raw_fif(raw_fname)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
picks = picks[1:13:3]
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), preload=True)
epochs_data = epochs.get_data(copy=False)
psd = PSDEstimator(2 * np.pi, 0, np.inf)
y = epochs.events[:, -1]
assert not hasattr(psd, 'fitted_')
X = psd.fit_transform(epochs_data, y)
assert psd.fitted_
assert X.shape[0] == epochs_data.shape[0]
assert_array_equal(psd.fit(epochs_data, y).transform(epochs_data), X)
with pytest.raises(ValueError):
    psd.fit('foo', y)
with pytest.raises(ValueError):
    psd.transform('foo')
```

## Next Steps


---

*Source: test_transformer.py:178 | Complexity: Advanced | Last updated: 2026-05-18*