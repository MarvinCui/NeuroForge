# How To: Position Information

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading file with 3 channels - one without position information.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `time`
- `copy`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.annotations`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.io.eeglab._eeglab`
- `mne.io.eeglab.eeglab`
- `mne.io.tests.test_raw`
- `mne.utils`
- `eeglabio.raw`

**Setup Required:**
```python
# Fixtures: three_chanpos_fname
```

## Step-by-Step Guide

### Step 1: 'Test reading file with 3 channels - one without position information.'

```python
'Test reading file with 3 channels - one without position information.'
```

**Verification:**
```python
assert_array_equal(np.array([ch['loc'] for ch in raw.info['chs']]), EXPECTED_LOCATIONS_FROM_FILE)
```

### Step 2: Assign nan = value

```python
nan = np.nan
```

### Step 3: Assign EXPECTED_LOCATIONS_FROM_FILE = value

```python
EXPECTED_LOCATIONS_FROM_FILE = np.array([[-4.0, 1.0, 7.0, 0.0, 0.0, 0.0, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [-5.0, 2.0, 8.0, 0.0, 0.0, 0.0, nan, nan, nan, nan, nan, nan]]) * 0.01
```

### Step 4: Assign EXPECTED_LOCATIONS_FROM_MONTAGE = np.array(...)

```python
EXPECTED_LOCATIONS_FROM_MONTAGE = np.array([[nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan]])
```

### Step 5: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(input_fname=three_chanpos_fname, preload=True, montage_units='cm')
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(np.array([ch['loc'] for ch in raw.info['chs']]), EXPECTED_LOCATIONS_FROM_FILE)
```

### Step 7: Assign raw = read_raw_eeglab.set_montage(...)

```python
raw = read_raw_eeglab(input_fname=three_chanpos_fname, preload=True, montage_units='cm').set_montage(None)
```

### Step 8: Call _assert_array_allclose_nan()

```python
_assert_array_allclose_nan(np.array([ch['loc'] for ch in raw.info['chs']]), EXPECTED_LOCATIONS_FROM_MONTAGE)
```


## Complete Example

```python
# Setup
# Fixtures: three_chanpos_fname

# Workflow
'Test reading file with 3 channels - one without position information.'
nan = np.nan
EXPECTED_LOCATIONS_FROM_FILE = np.array([[-4.0, 1.0, 7.0, 0.0, 0.0, 0.0, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [-5.0, 2.0, 8.0, 0.0, 0.0, 0.0, nan, nan, nan, nan, nan, nan]]) * 0.01
EXPECTED_LOCATIONS_FROM_MONTAGE = np.array([[nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan], [nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan, nan]])
raw = read_raw_eeglab(input_fname=three_chanpos_fname, preload=True, montage_units='cm')
assert_array_equal(np.array([ch['loc'] for ch in raw.info['chs']]), EXPECTED_LOCATIONS_FROM_FILE)
raw = read_raw_eeglab(input_fname=three_chanpos_fname, preload=True, montage_units='cm').set_montage(None)
_assert_array_allclose_nan(np.array([ch['loc'] for ch in raw.info['chs']]), EXPECTED_LOCATIONS_FROM_MONTAGE)
```

## Next Steps


---

*Source: test_eeglab.py:553 | Complexity: Advanced | Last updated: 2026-05-18*