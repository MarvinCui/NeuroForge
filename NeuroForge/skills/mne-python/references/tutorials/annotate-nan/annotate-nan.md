# How To: Annotate Nan

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests automatic NaN annotation generation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.preprocessing`

**Setup Required:**
```python
# Fixtures: meas_date
```

## Step-by-Step Guide

### Step 1: 'Tests automatic NaN annotation generation.'

```python
'Tests automatic NaN annotation generation.'
```

**Verification:**
```python
assert not np.isnan(raw._data).any()
```

### Step 2: Assign raw = mne.io.read_raw_fif(...)

```python
raw = mne.io.read_raw_fif(raw_fname)
```

**Verification:**
```python
assert len(annot_nan) == 0
```

### Step 3: Assign sfreq = 100

```python
sfreq = 100
```

**Verification:**
```python
assert annot_nan.orig_time == raw.info['meas_date']
```

### Step 4: Call raw.resample()

```python
raw.resample(sfreq)
```

**Verification:**
```python
assert_array_equal(annot_nan.onset, onset)
```

### Step 5: Assign annot_nan = annotate_nan(...)

```python
annot_nan = annotate_nan(raw)
```

**Verification:**
```python
assert_array_equal(annot_nan.duration, np.array([2]))
```

### Step 6: Assign nan_ch_idx = 0

```python
nan_ch_idx = 0
```

**Verification:**
```python
assert_array_equal(annot_nan.description, np.array(['BAD_NAN']))
```

### Step 7: Assign unknown = value

```python
raw._data[nan_ch_idx, 1 * sfreq:3 * sfreq] = np.nan
```

**Verification:**
```python
assert len(annot_nan.ch_names) == 1
```

### Step 8: Assign annot_nan = annotate_nan(...)

```python
annot_nan = annotate_nan(raw)
```

**Verification:**
```python
assert annot_nan.ch_names[0] == (raw.ch_names[nan_ch_idx],)
```

### Step 9: Assign onset = np.array(...)

```python
onset = np.array([1.0])
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(annot_nan.onset, onset)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(annot_nan.duration, np.array([2]))
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(annot_nan.description, np.array(['BAD_NAN']))
```

**Verification:**
```python
assert len(annot_nan.ch_names) == 1
```

### Step 13: Call raw.set_annotations()

```python
raw.set_annotations(annot_nan)
```

### Step 14: Call raw.set_meas_date()

```python
raw.set_meas_date(None)
```


## Complete Example

```python
# Setup
# Fixtures: meas_date

# Workflow
'Tests automatic NaN annotation generation.'
raw = mne.io.read_raw_fif(raw_fname)
sfreq = 100
raw.resample(sfreq)
if meas_date is None:
    raw.set_meas_date(None)
assert not np.isnan(raw._data).any()
annot_nan = annotate_nan(raw)
assert len(annot_nan) == 0
assert annot_nan.orig_time == raw.info['meas_date']
nan_ch_idx = 0
raw._data[nan_ch_idx, 1 * sfreq:3 * sfreq] = np.nan
annot_nan = annotate_nan(raw)
onset = np.array([1.0])
if raw.info['meas_date']:
    onset += raw.first_time
assert_array_equal(annot_nan.onset, onset)
assert_array_equal(annot_nan.duration, np.array([2]))
assert_array_equal(annot_nan.description, np.array(['BAD_NAN']))
assert len(annot_nan.ch_names) == 1
assert annot_nan.ch_names[0] == (raw.ch_names[nan_ch_idx],)
raw.set_annotations(annot_nan)
```

## Next Steps


---

*Source: test_annotate_nan.py:18 | Complexity: Advanced | Last updated: 2026-05-18*