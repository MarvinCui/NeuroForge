# How To: Meas Date

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test meas date conversion.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.egi.egi`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, timestamp, utc_offset
```

## Step-by-Step Guide

### Step 1: 'Test meas date conversion.'

```python
'Test meas date conversion.'
```

**Verification:**
```python
assert raw.info['meas_date'] == measdate
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert raw.info['utc_offset'] == utc_offset
```

### Step 3: Assign raw = read_raw_egi(...)

```python
raw = read_raw_egi(fname, verbose='warning')
```

**Verification:**
```python
assert local_utc_diff == int(utc_offset[:-2])
```

### Step 4: Assign dt = datetime.strptime(...)

```python
dt = datetime.strptime(timestamp, '%Y-%m-%dT%H:%M:%S.%f%z')
```

### Step 5: Assign measdate = dt.astimezone(...)

```python
measdate = dt.astimezone(timezone.utc)
```

### Step 6: Assign hour_local = int(...)

```python
hour_local = int(dt.strftime('%H'))
```

### Step 7: Assign hour_utc = int(...)

```python
hour_utc = int(raw.info['meas_date'].strftime('%H'))
```

### Step 8: Assign local_utc_diff = value

```python
local_utc_diff = hour_local - hour_utc
```

**Verification:**
```python
assert raw.info['meas_date'] == measdate
```


## Complete Example

```python
# Setup
# Fixtures: fname, timestamp, utc_offset

# Workflow
'Test meas date conversion.'
pytest.importorskip('defusedxml')
raw = read_raw_egi(fname, verbose='warning')
dt = datetime.strptime(timestamp, '%Y-%m-%dT%H:%M:%S.%f%z')
measdate = dt.astimezone(timezone.utc)
hour_local = int(dt.strftime('%H'))
hour_utc = int(raw.info['meas_date'].strftime('%H'))
local_utc_diff = hour_local - hour_utc
assert raw.info['meas_date'] == measdate
assert raw.info['utc_offset'] == utc_offset
assert local_utc_diff == int(utc_offset[:-2])
```

## Next Steps


---

*Source: test_egi.py:543 | Complexity: Advanced | Last updated: 2026-05-18*