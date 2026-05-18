# How To: Epochs Bad Baseline

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Epochs initialization with bad baseline parameters.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `datetime`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy.fft`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne._fiff.write`
- `mne.annotations`
- `mne.baseline`
- `mne.chpi`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas`


## Step-by-Step Guide

### Step 1: 'Test Epochs initialization with bad baseline parameters.'

```python
'Test Epochs initialization with bad baseline parameters.'
```

### Step 2: Assign unknown = value

```python
raw, events = _get_data()[:2]
```

### Step 3: Call pytest.raises()

```python
pytest.raises(ValueError, Epochs, raw, events, None, -0.1, 0.3, (0.1, 0))
```

### Step 4: Call pytest.raises()

```python
pytest.raises(ValueError, Epochs, raw, events, None, 0.1, 0.3, (None, 0))
```

### Step 5: Call pytest.raises()

```python
pytest.raises(ValueError, Epochs, raw, events, None, -0.3, -0.1, (0, None))
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, 0.1, 0.3, baseline=None)
```

### Step 7: Call epochs.load_data()

```python
epochs.load_data()
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, epochs.apply_baseline, (None, 0))
```

### Step 9: Call pytest.raises()

```python
pytest.raises(ValueError, epochs.apply_baseline, (0, None))
```

### Step 10: Assign data = np.arange(...)

```python
data = np.arange(100, dtype=float)
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, rescale, data, times=data, baseline=(-2, -1))
```

### Step 12: Call rescale()

```python
rescale(data.copy(), times=data, baseline=(2, 2))
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, rescale, data, times=data, baseline=(2, 1))
```

### Step 14: Call pytest.raises()

```python
pytest.raises(ValueError, rescale, data, times=data, baseline=(100, 101))
```

### Step 15: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, -0.1, 0.3, (-0.2, 0))
```

### Step 16: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, -0.1, 0.3, (0, 0.4))
```


## Complete Example

```python
# Workflow
'Test Epochs initialization with bad baseline parameters.'
raw, events = _get_data()[:2]
with pytest.raises(ValueError, match='interval.*outside of epochs data'):
    epochs = Epochs(raw, events, None, -0.1, 0.3, (-0.2, 0))
with pytest.raises(ValueError, match='interval.*outside of epochs data'):
    epochs = Epochs(raw, events, None, -0.1, 0.3, (0, 0.4))
pytest.raises(ValueError, Epochs, raw, events, None, -0.1, 0.3, (0.1, 0))
pytest.raises(ValueError, Epochs, raw, events, None, 0.1, 0.3, (None, 0))
pytest.raises(ValueError, Epochs, raw, events, None, -0.3, -0.1, (0, None))
epochs = Epochs(raw, events, None, 0.1, 0.3, baseline=None)
epochs.load_data()
pytest.raises(ValueError, epochs.apply_baseline, (None, 0))
pytest.raises(ValueError, epochs.apply_baseline, (0, None))
data = np.arange(100, dtype=float)
pytest.raises(ValueError, rescale, data, times=data, baseline=(-2, -1))
rescale(data.copy(), times=data, baseline=(2, 2))
pytest.raises(ValueError, rescale, data, times=data, baseline=(2, 1))
pytest.raises(ValueError, rescale, data, times=data, baseline=(100, 101))
```

## Next Steps


---

*Source: test_epochs.py:1171 | Complexity: Advanced | Last updated: 2026-05-18*