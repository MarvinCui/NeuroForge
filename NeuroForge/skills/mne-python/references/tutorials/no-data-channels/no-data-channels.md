# How To: No Data Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can load with no data channels.

## Prerequisites

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that we can load with no data channels.'

```python
'Test that we can load with no data channels.'
```

**Verification:**
```python
assert list(picks) == [len(raw.ch_names) - 1]
```

### Step 2: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path, preload=True)
```

**Verification:**
```python
assert_array_equal(stim_data, stim_data_2)
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, stim=True)
```

**Verification:**
```python
assert picks.size == 0
```

### Step 4: Assign stim_data = value

```python
stim_data = raw[picks][0]
```

### Step 5: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path, exclude=raw.ch_names[:-1])
```

### Step 6: Assign stim_data_2 = value

```python
stim_data_2 = raw[0][0]
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(stim_data, stim_data_2)
```

### Step 8: Call raw.plot()

```python
raw.plot()
```

### Step 9: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_overlap_annot_path)
```

### Step 10: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, stim=True)
```

**Verification:**
```python
assert picks.size == 0
```

### Step 11: Assign annot = value

```python
annot = raw.annotations
```

### Step 12: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_overlap_annot_path, exclude=raw.ch_names)
```

### Step 13: Assign annot_2 = value

```python
annot_2 = raw.annotations
```

### Step 14: Call _assert_annotations_equal()

```python
_assert_annotations_equal(annot, annot_2)
```

### Step 15: Call read_raw_edf()

```python
read_raw_edf(edf_annot_only)
```


## Complete Example

```python
# Workflow
'Test that we can load with no data channels.'
raw = read_raw_edf(edf_path, preload=True)
picks = pick_types(raw.info, stim=True)
assert list(picks) == [len(raw.ch_names) - 1]
stim_data = raw[picks][0]
raw = read_raw_edf(edf_path, exclude=raw.ch_names[:-1])
stim_data_2 = raw[0][0]
assert_array_equal(stim_data, stim_data_2)
raw.plot()
raw = read_raw_edf(edf_overlap_annot_path)
picks = pick_types(raw.info, stim=True)
assert picks.size == 0
annot = raw.annotations
raw = read_raw_edf(edf_overlap_annot_path, exclude=raw.ch_names)
annot_2 = raw.annotations
_assert_annotations_equal(annot, annot_2)
with _record_warnings(), pytest.warns(RuntimeWarning, match='read_annotations'):
    read_raw_edf(edf_annot_only)
```

## Next Steps


---

*Source: test_edf.py:393 | Complexity: Advanced | Last updated: 2026-05-18*