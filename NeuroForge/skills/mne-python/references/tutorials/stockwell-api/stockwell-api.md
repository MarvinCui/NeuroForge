# How To: Stockwell Api

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test stockwell functions.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency._stockwell`
- `mne.utils`

**Required Fixtures:**
- `api_client` fixture


## Step-by-Step Guide

### Step 1: 'Test stockwell functions.'

```python
'Test stockwell functions.'
```

**Verification:**
```python
assert power.freqs.max() <= fmax
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_almost_equal(power_evoked.data, power.data)
```

### Step 3: Assign unknown = value

```python
event_id, tmin, tmax = (1, -0.2, 0.5)
```

**Verification:**
```python
assert isinstance(power, AverageTFR)
```

### Step 4: Assign event_name = value

```python
event_name = base_dir / 'test-eve.fif'
```

**Verification:**
```python
assert isinstance(itc, AverageTFR)
```

### Step 5: Assign events = read_events(...)

```python
events = read_events(event_name)
```

**Verification:**
```python
assert_equal(power.data.shape, itc.data.shape)
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=[0, 1, 3])
```

**Verification:**
```python
assert itc.data.min() >= 0.0
```

### Step 7: Call assert_equal()

```python
assert_equal(power.data.shape, itc.data.shape)
```

**Verification:**
```python
assert itc.data.max() <= 1.0
```

### Step 8: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(1, 1024)
```

**Verification:**
```python
assert np.log(power.data.max()) * 20 <= 0.0
```

### Step 9: Assign data = value

```python
data = data[np.newaxis]
```

**Verification:**
```python
assert np.log(power.data.max()) * 20 <= 0.0
```

### Step 10: Assign unknown = tfr_array_stockwell(...)

```python
power, itc, freqs = tfr_array_stockwell(data, 1000.0, return_itc=True)
```

**Verification:**
```python
assert_allclose(itc, np.ones_like(itc))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(itc, np.ones_like(itc))
```

**Verification:**
```python
assert power.shape == (1, len(freqs), data.shape[-1])
```

### Step 12: Call assert_array_less()

```python
assert_array_less(0, power)
```

**Verification:**
```python
assert_array_less(0, power)
```

### Step 13: Assign unknown = tfr_stockwell(...)

```python
power, itc = tfr_stockwell(epochs, fmin=fmin, fmax=fmax, return_itc=True)
```

### Step 14: Assign power_evoked = tfr_stockwell(...)

```python
power_evoked = tfr_stockwell(epochs.average(), fmin=fmin, fmax=fmax, return_itc=False)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(power_evoked.data, power.data)
```

### Step 16: Call tfr_array_stockwell()

```python
tfr_array_stockwell('foo', 1000.0)
```

### Step 17: Call tfr_array_stockwell()

```python
tfr_array_stockwell(data, 1000.0)
```

**Verification:**
```python
assert power.freqs.max() <= fmax
```


## Complete Example

```python
# Workflow
'Test stockwell functions.'
raw = read_raw_fif(raw_fname)
event_id, tmin, tmax = (1, -0.2, 0.5)
event_name = base_dir / 'test-eve.fif'
events = read_events(event_name)
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=[0, 1, 3])
for fmin, fmax in [(None, 50), (5, 50), (5, None)]:
    power, itc = tfr_stockwell(epochs, fmin=fmin, fmax=fmax, return_itc=True)
    if fmax is not None:
        assert power.freqs.max() <= fmax
    power_evoked = tfr_stockwell(epochs.average(), fmin=fmin, fmax=fmax, return_itc=False)
    assert_array_almost_equal(power_evoked.data, power.data)
assert isinstance(power, AverageTFR)
assert isinstance(itc, AverageTFR)
assert_equal(power.data.shape, itc.data.shape)
assert itc.data.min() >= 0.0
assert itc.data.max() <= 1.0
assert np.log(power.data.max()) * 20 <= 0.0
assert np.log(power.data.max()) * 20 <= 0.0
with pytest.raises(TypeError, match='ndarray'):
    tfr_array_stockwell('foo', 1000.0)
data = np.random.RandomState(0).randn(1, 1024)
with pytest.raises(ValueError, match='3D with shape'):
    tfr_array_stockwell(data, 1000.0)
data = data[np.newaxis]
power, itc, freqs = tfr_array_stockwell(data, 1000.0, return_itc=True)
assert_allclose(itc, np.ones_like(itc))
assert power.shape == (1, len(freqs), data.shape[-1])
assert_array_less(0, power)
```

## Next Steps


---

*Source: test_stockwell.py:111 | Complexity: Advanced | Last updated: 2026-05-18*