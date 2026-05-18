# How To: Xdawn Fit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Xdawn fit.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.io`
- `mne.decoding.xdawn`
- `mne.preprocessing.xdawn`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `mne.decoding`


## Step-by-Step Guide

### Step 1: 'Test Xdawn fit.'

```python
'Test Xdawn fit.'
```

**Verification:**
```python
assert not xd.correct_overlap_
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, events, picks = _get_data()
```

**Verification:**
```python
assert_array_equal(evoked.data, xd.evokeds_['cond2'].data)
```

### Step 3: Call raw.del_proj()

```python
raw.del_proj()
```

**Verification:**
```python
assert_allclose(np.linalg.norm(xd.filters_['cond2'], axis=1), 1)
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=None, verbose=False)
```

### Step 5: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap='auto')
```

### Step 6: Call xd.fit()

```python
xd.fit(epochs)
```

**Verification:**
```python
assert not xd.correct_overlap_
```

### Step 7: Assign evoked = unknown.average(...)

```python
evoked = epochs['cond2'].average()
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(evoked.data, xd.evokeds_['cond2'].data)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(xd.filters_['cond2'], axis=1), 1)
```

### Step 10: Assign signal_cov = compute_raw_covariance(...)

```python
signal_cov = compute_raw_covariance(raw, picks=picks)
```

### Step 11: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
```

### Step 12: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 13: Assign signal_cov = np.eye(...)

```python
signal_cov = np.eye(len(picks))
```

### Step 14: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
```

### Step 15: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 16: Assign signal_cov = np.eye(...)

```python
signal_cov = np.eye(len(picks) - 1)
```

### Step 17: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
```

### Step 18: Call pytest.raises()

```python
pytest.raises(ValueError, xd.fit, epochs)
```

### Step 19: Assign signal_cov = 42

```python
signal_cov = 42
```

### Step 20: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
```

### Step 21: Call pytest.raises()

```python
pytest.raises(ValueError, xd.fit, epochs)
```

### Step 22: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=(None, 0), verbose=False)
```

### Step 23: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=2, correct_overlap=True)
```

### Step 24: Call pytest.raises()

```python
pytest.raises(ValueError, xd.fit, epochs)
```


## Complete Example

```python
# Workflow
'Test Xdawn fit.'
raw, events, picks = _get_data()
raw.del_proj()
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=None, verbose=False)
xd = Xdawn(n_components=2, correct_overlap='auto')
xd.fit(epochs)
assert not xd.correct_overlap_
evoked = epochs['cond2'].average()
assert_array_equal(evoked.data, xd.evokeds_['cond2'].data)
assert_allclose(np.linalg.norm(xd.filters_['cond2'], axis=1), 1)
signal_cov = compute_raw_covariance(raw, picks=picks)
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
xd.fit(epochs)
signal_cov = np.eye(len(picks))
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
xd.fit(epochs)
signal_cov = np.eye(len(picks) - 1)
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
pytest.raises(ValueError, xd.fit, epochs)
signal_cov = 42
xd = Xdawn(n_components=2, correct_overlap=False, signal_cov=signal_cov)
pytest.raises(ValueError, xd.fit, epochs)
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=(None, 0), verbose=False)
xd = Xdawn(n_components=2, correct_overlap=True)
pytest.raises(ValueError, xd.fit, epochs)
```

## Next Steps


---

*Source: test_xdawn.py:68 | Complexity: Advanced | Last updated: 2026-05-18*