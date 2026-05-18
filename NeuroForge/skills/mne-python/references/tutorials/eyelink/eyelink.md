# How To: Eyelink

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading eyelink asc files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.eyelink._utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, create_annotations, find_overlaps, apply_offsets
```

## Step-by-Step Guide

### Step 1: 'Test reading eyelink asc files.'

```python
'Test reading eyelink asc files.'
```

**Verification:**
```python
assert raw.info['sfreq'] == 500
```

### Step 2: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(fname, create_annotations=create_annotations, find_overlaps=find_overlaps, apply_offsets=apply_offsets)
```

**Verification:**
```python
assert raw.info['meas_date'].month == 3
```

### Step 3: raw.info['chs'][2]['coil_type'] == FIFF.FIFFV_COIL_EYETRACK_PUPIL

```python
raw.info['chs'][2]['coil_type'] == FIFF.FIFFV_COIL_EYETRACK_PUPIL
```

**Verification:**
```python
assert raw.info['meas_date'].day == 10
```

### Step 4: Assign orig = value

```python
orig = raw.info['meas_date']
```

**Verification:**
```python
assert raw.info['meas_date'].year == 2022
```

### Step 5: Assign df = raw.annotations.to_data_frame(...)

```python
df = raw.annotations.to_data_frame()
```

**Verification:**
```python
assert len(raw.info['ch_names']) == 6
```

### Step 6: Assign unknown = unknown.apply(...)

```python
df['time_in_sec'] = df['onset'].apply(lambda x: x.timestamp() - orig.timestamp())
```

**Verification:**
```python
assert raw.info['chs'][0]['kind'] == FIFF.FIFFV_EYETRACK_CH
```

### Step 7: Assign cond = value

```python
cond = (df['time_in_sec'] > 8.899) & (df['time_in_sec'] < 8.95)
```

**Verification:**
```python
assert raw.info['chs'][0]['coil_type'] == FIFF.FIFFV_COIL_EYETRACK_POS
```


## Complete Example

```python
# Setup
# Fixtures: fname, create_annotations, find_overlaps, apply_offsets

# Workflow
'Test reading eyelink asc files.'
raw = read_raw_eyelink(fname, create_annotations=create_annotations, find_overlaps=find_overlaps, apply_offsets=apply_offsets)
assert raw.info['sfreq'] == 500
assert raw.info['meas_date'].month == 3
assert raw.info['meas_date'].day == 10
assert raw.info['meas_date'].year == 2022
assert len(raw.info['ch_names']) == 6
assert raw.info['chs'][0]['kind'] == FIFF.FIFFV_EYETRACK_CH
assert raw.info['chs'][0]['coil_type'] == FIFF.FIFFV_COIL_EYETRACK_POS
raw.info['chs'][2]['coil_type'] == FIFF.FIFFV_COIL_EYETRACK_PUPIL
assert all(raw.info['chs'][0]['loc'][3:5] == [-1, -1])
assert raw.info['chs'][2]['loc'][3] == -1
assert np.isnan(raw.info['chs'][2]['loc'][4])
assert all(raw.info['chs'][4]['loc'][3:5] == [1, 1])
assert 'RawEyelink' in repr(raw)
if create_annotations is True and find_overlaps:
    orig = raw.info['meas_date']
    df = raw.annotations.to_data_frame()
    df['time_in_sec'] = df['onset'].apply(lambda x: x.timestamp() - orig.timestamp())
    cond = (df['time_in_sec'] > 8.899) & (df['time_in_sec'] < 8.95)
    assert df[cond]['description'].values[0].startswith('BAD_blink')
    assert np.array_equal(raw.annotations[0]['ch_names'], MAPPING['both'])
if isinstance(create_annotations, list) and find_overlaps:
    assert np.array_equal(raw.annotations[0]['ch_names'], MAPPING['both'])
```

## Next Steps


---

*Source: test_eyelink.py:82 | Complexity: Intermediate | Last updated: 2026-05-18*