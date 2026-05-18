# How To: Double Export Edf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test exporting an EDF file multiple times.

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

### Step 1: 'Test exporting an EDF file multiple times.'

```python
'Test exporting an EDF file multiple times.'
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 2: Assign raw = _create_raw_for_edf_tests(...)

```python
raw = _create_raw_for_edf_tests(stim_channel_index=2)
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 3: Call raw.info.set_meas_date()

```python
raw.info.set_meas_date(datetime(2023, 9, 4, 14, 53, 9, tzinfo=timezone.utc))
```

**Verification:**
```python
assert_array_equal(raw.times, raw_read.times)
```

### Step 4: Call raw.set_annotations()

```python
raw.set_annotations(Annotations(onset=[1], duration=[0], description=['test']))
```

**Verification:**
```python
assert raw.info[key] == raw_read.info[key]
```

### Step 5: Assign unknown = dict(...)

```python
raw.info['subject_info'] = dict(his_id='12345', first_name='mne', last_name='python', birthday=date(1992, 1, 20), sex=1, weight=78.3, height=1.75, hand=3)
```

**Verification:**
```python
assert_array_equal(orig_ch_types, read_ch_types)
```

### Step 6: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.edf'
```

### Step 7: Call raw.export()

```python
raw.export(temp_fname, add_ch_type=True)
```

### Step 8: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
```

### Step 9: Call raw_read.export()

```python
raw_read.export(temp_fname, add_ch_type=True, overwrite=True)
```

### Step 10: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(raw.times, raw_read.times)
```

### Step 13: Assign orig_ch_types = raw.get_channel_types(...)

```python
orig_ch_types = raw.get_channel_types()
```

### Step 14: Assign read_ch_types = raw_read.get_channel_types(...)

```python
read_ch_types = raw_read.get_channel_types()
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(orig_ch_types, read_ch_types)
```

**Verification:**
```python
assert raw.info[key] == raw_read.info[key]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test exporting an EDF file multiple times.'
raw = _create_raw_for_edf_tests(stim_channel_index=2)
raw.info.set_meas_date(datetime(2023, 9, 4, 14, 53, 9, tzinfo=timezone.utc))
raw.set_annotations(Annotations(onset=[1], duration=[0], description=['test']))
raw.info['subject_info'] = dict(his_id='12345', first_name='mne', last_name='python', birthday=date(1992, 1, 20), sex=1, weight=78.3, height=1.75, hand=3)
temp_fname = tmp_path / 'test.edf'
raw.export(temp_fname, add_ch_type=True)
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
raw_read.export(temp_fname, add_ch_type=True, overwrite=True)
raw_read = read_raw_edf(temp_fname, infer_types=True, preload=True)
assert raw.ch_names == raw_read.ch_names
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
assert_array_equal(raw.times, raw_read.times)
for key in set(raw.info) - {'chs'}:
    assert raw.info[key] == raw_read.info[key]
orig_ch_types = raw.get_channel_types()
read_ch_types = raw_read.get_channel_types()
assert_array_equal(orig_ch_types, read_ch_types)
```

## Next Steps


---

*Source: test_export.py:198 | Complexity: Advanced | Last updated: 2026-05-18*