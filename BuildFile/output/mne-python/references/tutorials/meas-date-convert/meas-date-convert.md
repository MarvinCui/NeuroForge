# How To: Meas Date Convert

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test conversions of meas_date to datetime objects.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`

**Setup Required:**
```python
# Fixtures: stamp, dt
```

## Step-by-Step Guide

### Step 1: 'Test conversions of meas_date to datetime objects.'

```python
'Test conversions of meas_date to datetime objects.'
```

**Verification:**
```python
assert stamp == stamp2
```

### Step 2: Assign meas_datetime = _stamp_to_dt(...)

```python
meas_datetime = _stamp_to_dt(stamp)
```

**Verification:**
```python
assert meas_datetime == datetime(*dt, tzinfo=timezone.utc)
```

### Step 3: Assign stamp2 = _dt_to_stamp(...)

```python
stamp2 = _dt_to_stamp(meas_datetime)
```

**Verification:**
```python
assert str(dt[0]) in repr(info)
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(1, 1000.0, 'eeg')
```

**Verification:**
```python
assert str(dt[0]) in repr(info)
```

### Step 5: Assign unknown = meas_datetime

```python
info['meas_date'] = meas_datetime
```


## Complete Example

```python
# Setup
# Fixtures: stamp, dt

# Workflow
'Test conversions of meas_date to datetime objects.'
meas_datetime = _stamp_to_dt(stamp)
stamp2 = _dt_to_stamp(meas_datetime)
assert stamp == stamp2
assert meas_datetime == datetime(*dt, tzinfo=timezone.utc)
info = create_info(1, 1000.0, 'eeg')
with info._unlock():
    info['meas_date'] = meas_datetime
assert str(dt[0]) in repr(info)
```

## Next Steps


---

*Source: test_meas_info.py:936 | Complexity: Intermediate | Last updated: 2026-05-18*