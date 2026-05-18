# How To: Eeglab Read Annotations

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test annotations onsets are timestamps (+ validate some).

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test annotations onsets are timestamps (+ validate some).'

```python
'Test annotations onsets are timestamps (+ validate some).'
```

**Verification:**
```python
assert annotations.orig_time is None
```

### Step 2: Assign annotations = read_annotations(...)

```python
annotations = read_annotations(raw_fname_mat)
```

**Verification:**
```python
assert_array_almost_equal(annotations.onset[validation_samples], expected_onset, decimal=2)
```

### Step 3: Assign validation_samples = value

```python
validation_samples = [0, 1, 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31]
```

**Verification:**
```python
assert_allclose(raw.annotations.duration, np.ones(3) * 0.5)
```

### Step 4: Assign expected_onset = np.array(...)

```python
expected_onset = np.array([1.0, 1.69, 2.08, 4.7, 7.71, 11.3, 17.18, 20.2, 26.12, 29.14, 35.25, 44.3, 47.15])
```

**Verification:**
```python
assert annotations.orig_time is None
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(annotations.onset[validation_samples], expected_onset, decimal=2)
```

### Step 6: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(raw_fname_event_duration, preload=True, montage_units='dm')
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw.annotations.duration, np.ones(3) * 0.5)
```


## Complete Example

```python
# Workflow
'Test annotations onsets are timestamps (+ validate some).'
annotations = read_annotations(raw_fname_mat)
validation_samples = [0, 1, 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31]
expected_onset = np.array([1.0, 1.69, 2.08, 4.7, 7.71, 11.3, 17.18, 20.2, 26.12, 29.14, 35.25, 44.3, 47.15])
assert annotations.orig_time is None
assert_array_almost_equal(annotations.onset[validation_samples], expected_onset, decimal=2)
raw = read_raw_eeglab(raw_fname_event_duration, preload=True, montage_units='dm')
assert_allclose(raw.annotations.duration, np.ones(3) * 0.5)
```

## Next Steps


---

*Source: test_eeglab.py:461 | Complexity: Intermediate | Last updated: 2026-05-18*