# How To: Xdawn Apply Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Xdawn apply and transform.

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

### Step 1: 'Test Xdawn apply and transform.'

```python
'Test Xdawn apply and transform.'
```

**Verification:**
```python
assert_array_almost_equal(denoise['cond2']._data, denoise_shfl['cond2']._data)
```

### Step 2: Assign unknown = _get_data(...)

```python
raw, events, picks = _get_data()
```

### Step 3: Call raw.pick()

```python
raw.pick(picks='eeg')
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, proj=False, preload=True, baseline=None, verbose=False)
```

### Step 5: Assign n_components = 2

```python
n_components = 2
```

### Step 6: Assign xd = Xdawn(...)

```python
xd = Xdawn(n_components=n_components, correct_overlap=False)
```

### Step 7: Call xd.fit()

```python
xd.fit(epochs)
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, xd.apply, 42)
```

### Step 9: Call xd.transform()

```python
xd.transform(epochs)
```

### Step 10: Call xd.transform()

```python
xd.transform(epochs.average())
```

### Step 11: Call xd.transform()

```python
xd.transform(epochs._data)
```

### Step 12: Call xd.transform()

```python
xd.transform(epochs._data[0])
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, xd.transform, 42)
```

### Step 14: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 15: Assign idx = np.arange(...)

```python
idx = np.arange(len(epochs))
```

### Step 16: Call rng.shuffle()

```python
rng.shuffle(idx)
```

### Step 17: Call xd.fit()

```python
xd.fit(epochs[idx])
```

### Step 18: Assign denoise_shfl = xd.apply(...)

```python
denoise_shfl = xd.apply(epochs)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(denoise['cond2']._data, denoise_shfl['cond2']._data)
```

### Step 20: Assign denoise = xd.apply(...)

```python
denoise = xd.apply(inst)
```


## Complete Example

```python
# Workflow
'Test Xdawn apply and transform.'
raw, events, picks = _get_data()
raw.pick(picks='eeg')
epochs = Epochs(raw, events, event_id, tmin, tmax, proj=False, preload=True, baseline=None, verbose=False)
n_components = 2
xd = Xdawn(n_components=n_components, correct_overlap=False)
xd.fit(epochs)
for inst in [raw, epochs.average(), epochs]:
    denoise = xd.apply(inst)
pytest.raises(ValueError, xd.apply, 42)
xd.transform(epochs)
xd.transform(epochs.average())
xd.transform(epochs._data)
xd.transform(epochs._data[0])
pytest.raises(ValueError, xd.transform, 42)
rng = np.random.RandomState(0)
idx = np.arange(len(epochs))
rng.shuffle(idx)
xd.fit(epochs[idx])
denoise_shfl = xd.apply(epochs)
assert_array_almost_equal(denoise['cond2']._data, denoise_shfl['cond2']._data)
```

## Next Steps


---

*Source: test_xdawn.py:132 | Complexity: Advanced | Last updated: 2026-05-18*