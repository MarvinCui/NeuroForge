# How To: Rawarray Edf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test saving a Raw array with integer sfreq to EDF.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.export`
- `mne.fixes`
- `mne.io`
- `mne.tests.test_epochs`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test saving a Raw array with integer sfreq to EDF.'

```python
'Test saving a Raw array with integer sfreq to EDF.'
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 2: Assign raw = _create_raw_for_edf_tests(...)

```python
raw = _create_raw_for_edf_tests()
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 3: Assign unknown = dict(...)

```python
raw.info['subject_info'] = dict(first_name='mne', last_name='python', birthday=date(1992, 1, 20), sex=1, hand=3)
```

**Verification:**
```python
assert_array_equal(raw.times, raw_read.times)
```

### Step 4: Assign time_now = datetime.now(...)

```python
time_now = datetime.now()
```

**Verification:**
```python
assert_array_equal(orig_ch_types, read_ch_types)
```

### Step 5: Assign meas_date = datetime(...)

```python
meas_date = datetime(year=time_now.year, month=time_now.month, day=time_now.day, hour=time_now.hour, minute=time_now.minute, second=time_now.second, tzinfo=timezone.utc)
```

**Verification:**
```python
assert raw.info['meas_date'] == raw_read.info['meas_date']
```

### Step 6: Call raw.set_meas_date()

```python
raw.set_meas_date(meas_date)
```

### Step 7: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.edf'
```

### Step 8: Call raw.export()

```python
raw.export(temp_fname, add_ch_type=True)
```

### Step 9: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(raw.times, raw_read.times)
```

### Step 12: Assign orig_ch_types = raw.get_channel_types(...)

```python
orig_ch_types = raw.get_channel_types()
```

### Step 13: Assign read_ch_types = raw_read.get_channel_types(...)

```python
read_ch_types = raw_read.get_channel_types()
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(orig_ch_types, read_ch_types)
```

**Verification:**
```python
assert raw.info['meas_date'] == raw_read.info['meas_date']
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test saving a Raw array with integer sfreq to EDF.'
raw = _create_raw_for_edf_tests()
raw.info['subject_info'] = dict(first_name='mne', last_name='python', birthday=date(1992, 1, 20), sex=1, hand=3)
time_now = datetime.now()
meas_date = datetime(year=time_now.year, month=time_now.month, day=time_now.day, hour=time_now.hour, minute=time_now.minute, second=time_now.second, tzinfo=timezone.utc)
raw.set_meas_date(meas_date)
temp_fname = tmp_path / 'test.edf'
raw.export(temp_fname, add_ch_type=True)
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
assert raw.ch_names == raw_read.ch_names
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
assert_array_equal(raw.times, raw_read.times)
orig_ch_types = raw.get_channel_types()
read_ch_types = raw_read.get_channel_types()
assert_array_equal(orig_ch_types, read_ch_types)
assert raw.info['meas_date'] == raw_read.info['meas_date']
```

## Next Steps


---

*Source: test_export.py:362 | Complexity: Advanced | Last updated: 2026-05-18*