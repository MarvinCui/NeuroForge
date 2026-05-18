# How To: Muscle Annotation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test correct detection muscle artifacts.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.chpi`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.tests.test_annotations`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: meas_date, events
```

## Step-by-Step Guide

### Step 1: 'Test correct detection muscle artifacts.'

```python
'Test correct detection muscle artifacts.'
```

**Verification:**
```python
assert annot_muscle.orig_time == raw.info['meas_date']
```

### Step 2: Assign raw = read_raw_fif.load_data(...)

```python
raw = read_raw_fif(raw_fname, allow_maxshield='yes').load_data()
```

**Verification:**
```python
assert_array_equal(scores[onset].astype(int), np.array([23, 10]))
```

### Step 3: Call raw.notch_filter()

```python
raw.notch_filter([50, 110, 150])
```

**Verification:**
```python
assert annot_muscle.duration.size == 2
```

### Step 4: Assign unknown = annotate_muscle_zscore(...)

```python
annot_muscle, scores = annotate_muscle_zscore(raw, ch_type='mag', threshold=10)
```

**Verification:**
```python
assert annot_muscle.orig_time == raw.info['meas_date']
```

### Step 5: Assign onset = value

```python
onset = annot_muscle.onset * raw.info['sfreq']
```

### Step 6: Assign onset = onset.astype(...)

```python
onset = onset.astype(int)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(scores[onset].astype(int), np.array([23, 10]))
```

**Verification:**
```python
assert annot_muscle.duration.size == 2
```

### Step 8: Call raw.set_annotations()

```python
raw.set_annotations(annot_muscle)
```

### Step 9: Call raw.set_meas_date()

```python
raw.set_meas_date(None)
```


## Complete Example

```python
# Setup
# Fixtures: meas_date, events

# Workflow
'Test correct detection muscle artifacts.'
raw = read_raw_fif(raw_fname, allow_maxshield='yes').load_data()
if meas_date is None:
    raw.set_meas_date(None)
raw.notch_filter([50, 110, 150])
annot_muscle, scores = annotate_muscle_zscore(raw, ch_type='mag', threshold=10)
assert annot_muscle.orig_time == raw.info['meas_date']
onset = annot_muscle.onset * raw.info['sfreq']
if meas_date is not None:
    onset -= raw.first_samp
onset = onset.astype(int)
assert_array_equal(scores[onset].astype(int), np.array([23, 10]))
assert annot_muscle.duration.size == 2
raw.set_annotations(annot_muscle)
```

## Next Steps


---

*Source: test_artifact_detection.py:162 | Complexity: Advanced | Last updated: 2026-05-18*