# How To: Subject Info

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading subject information.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `os`
- `pathlib`
- `pickle`
- `platform`
- `shutil`
- `contextlib`
- `copy`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading subject information.'

```python
'Test reading subject information.'
```

**Verification:**
```python
assert raw.info['subject_info'] is None
```

### Step 2: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(fif_fname).crop(0, 1)
```

**Verification:**
```python
assert subject_info[key] == raw_read.info['subject_info'][key]
```

### Step 3: Assign keys = value

```python
keys = ['id', 'his_id', 'last_name', 'first_name', 'birthday', 'sex', 'hand']
```

**Verification:**
```python
assert raw.info['meas_date'] == raw_read.info['meas_date']
```

### Step 4: Assign vals = value

```python
vals = [1, 'foobar', 'bar', 'foo', datetime.date(1901, 2, 3), 0, 1]
```

**Verification:**
```python
assert raw.info['meas_id'][key] == raw_read.info['meas_id'][key]
```

### Step 5: Assign subject_info = dict(...)

```python
subject_info = dict()
```

**Verification:**
```python
assert_array_equal(raw.info['meas_id']['machid'], raw_read.info['meas_id']['machid'])
```

### Step 6: Assign unknown = subject_info

```python
raw.info['subject_info'] = subject_info
```

### Step 7: Assign out_fname = value

```python
out_fname = tmp_path / 'test_subj_info_raw.fif'
```

### Step 8: Call raw.save()

```python
raw.save(out_fname, overwrite=True)
```

### Step 9: Assign raw_read = read_raw_fif(...)

```python
raw_read = read_raw_fif(out_fname)
```

**Verification:**
```python
assert raw.info['meas_date'] == raw_read.info['meas_date']
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(raw.info['meas_id']['machid'], raw_read.info['meas_id']['machid'])
```

### Step 11: Assign unknown = val

```python
subject_info[key] = val
```

**Verification:**
```python
assert subject_info[key] == raw_read.info['subject_info'][key]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading subject information.'
raw = read_raw_fif(fif_fname).crop(0, 1)
assert raw.info['subject_info'] is None
keys = ['id', 'his_id', 'last_name', 'first_name', 'birthday', 'sex', 'hand']
vals = [1, 'foobar', 'bar', 'foo', datetime.date(1901, 2, 3), 0, 1]
subject_info = dict()
for key, val in zip(keys, vals):
    subject_info[key] = val
raw.info['subject_info'] = subject_info
out_fname = tmp_path / 'test_subj_info_raw.fif'
raw.save(out_fname, overwrite=True)
raw_read = read_raw_fif(out_fname)
for key in keys:
    assert subject_info[key] == raw_read.info['subject_info'][key]
assert raw.info['meas_date'] == raw_read.info['meas_date']
for key in ['secs', 'usecs', 'version']:
    assert raw.info['meas_id'][key] == raw_read.info['meas_id'][key]
assert_array_equal(raw.info['meas_id']['machid'], raw_read.info['meas_id']['machid'])
```

## Next Steps


---

*Source: test_raw_fiff.py:189 | Complexity: Advanced | Last updated: 2026-05-18*