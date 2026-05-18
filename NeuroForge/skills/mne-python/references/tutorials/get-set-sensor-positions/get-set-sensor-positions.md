# How To: Get Set Sensor Positions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test get/set functions for sensor positions.

## Prerequisites

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test get/set functions for sensor positions.'

```python
'Test get/set functions for sensor positions.'
```

**Verification:**
```python
assert_array_equal(raw_pos, pos)
```

### Step 2: Assign raw1 = read_raw_fif(...)

```python
raw1 = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_equal(raw1.info['chs'][13]['loc'], raw2.info['chs'][13]['loc'])
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(raw1.info, meg=False, eeg=True)
```

### Step 4: Assign pos = value

```python
pos = np.array([ch['loc'][:3] for ch in raw1.info['chs']])[picks]
```

### Step 5: Assign raw_pos = raw1._get_channel_positions(...)

```python
raw_pos = raw1._get_channel_positions(picks=picks)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(raw_pos, pos)
```

### Step 7: Assign ch_name = value

```python
ch_name = raw1.info['ch_names'][13]
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, raw1._set_channel_positions, [1, 2], ['name'])
```

### Step 9: Assign raw2 = read_raw_fif(...)

```python
raw2 = read_raw_fif(raw_fname)
```

### Step 10: Assign unknown = np.array(...)

```python
raw2.info['chs'][13]['loc'][:3] = np.array([1, 2, 3])
```

### Step 11: Call raw1._set_channel_positions()

```python
raw1._set_channel_positions([[1, 2, 3]], [ch_name])
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(raw1.info['chs'][13]['loc'], raw2.info['chs'][13]['loc'])
```


## Complete Example

```python
# Workflow
'Test get/set functions for sensor positions.'
raw1 = read_raw_fif(raw_fname)
picks = pick_types(raw1.info, meg=False, eeg=True)
pos = np.array([ch['loc'][:3] for ch in raw1.info['chs']])[picks]
raw_pos = raw1._get_channel_positions(picks=picks)
assert_array_equal(raw_pos, pos)
ch_name = raw1.info['ch_names'][13]
pytest.raises(ValueError, raw1._set_channel_positions, [1, 2], ['name'])
raw2 = read_raw_fif(raw_fname)
raw2.info['chs'][13]['loc'][:3] = np.array([1, 2, 3])
raw1._set_channel_positions([[1, 2, 3]], [ch_name])
assert_array_equal(raw1.info['chs'][13]['loc'], raw2.info['chs'][13]['loc'])
```

## Next Steps


---

*Source: test_channels.py:386 | Complexity: Advanced | Last updated: 2026-05-18*