# How To: Get Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the get_data method for Evoked.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test the get_data method for Evoked.'

```python
'Test the get_data method for Evoked.'
```

**Verification:**
```python
assert_array_equal(d1, d2)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname, 0)
```

**Verification:**
```python
assert_array_equal(evoked.data[eeg_idxs], evoked.get_data(picks='eeg'))
```

### Step 3: Assign d1 = evoked.get_data(...)

```python
d1 = evoked.get_data()
```

**Verification:**
```python
assert np.all(d3.shape[1] == evoked.data.shape[1] - np.nonzero(evoked.times == 0)[0])
```

### Step 4: Assign d2 = value

```python
d2 = evoked.data
```

**Verification:**
```python
assert evoked.get_data(tmin=0, tmax=0).size == 0
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(d1, d2)
```

**Verification:**
```python
assert_array_equal(d1, d2)
```

### Step 6: Assign eeg_idxs = np.array(...)

```python
eeg_idxs = np.array([i == 'eeg' for i in evoked.get_channel_types()])
```

**Verification:**
```python
assert_array_equal(d1 * 1000000.0, d3)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(evoked.data[eeg_idxs], evoked.get_data(picks='eeg'))
```

### Step 8: Assign d3 = evoked.get_data(...)

```python
d3 = evoked.get_data(tmin=0)
```

**Verification:**
```python
assert np.all(d3.shape[1] == evoked.data.shape[1] - np.nonzero(evoked.times == 0)[0])
```

### Step 9: Assign d1 = evoked.get_data(...)

```python
d1 = evoked.get_data(picks='eeg', units=None)
```

### Step 10: Assign d2 = evoked.get_data(...)

```python
d2 = evoked.get_data(picks='eeg', units='V')
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(d1, d2)
```

### Step 12: Assign d3 = evoked.get_data(...)

```python
d3 = evoked.get_data(picks='eeg', units='µV')
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(d1 * 1000000.0, d3)
```

### Step 14: Call evoked.get_data()

```python
evoked.get_data(tmin=[1], tmax=1)
```

### Step 15: Call evoked.get_data()

```python
evoked.get_data(tmin=1, tmax=np.ones(5))
```


## Complete Example

```python
# Workflow
'Test the get_data method for Evoked.'
evoked = read_evokeds(fname, 0)
d1 = evoked.get_data()
d2 = evoked.data
assert_array_equal(d1, d2)
eeg_idxs = np.array([i == 'eeg' for i in evoked.get_channel_types()])
assert_array_equal(evoked.data[eeg_idxs], evoked.get_data(picks='eeg'))
d3 = evoked.get_data(tmin=0)
assert np.all(d3.shape[1] == evoked.data.shape[1] - np.nonzero(evoked.times == 0)[0])
assert evoked.get_data(tmin=0, tmax=0).size == 0
with pytest.raises(TypeError, match='tmin .* float, None'):
    evoked.get_data(tmin=[1], tmax=1)
with pytest.raises(TypeError, match='tmax .* float, None'):
    evoked.get_data(tmin=1, tmax=np.ones(5))
d1 = evoked.get_data(picks='eeg', units=None)
d2 = evoked.get_data(picks='eeg', units='V')
assert_array_equal(d1, d2)
d3 = evoked.get_data(picks='eeg', units='µV')
assert_array_equal(d1 * 1000000.0, d3)
```

## Next Steps


---

*Source: test_evoked.py:43 | Complexity: Advanced | Last updated: 2026-05-18*