# How To: Export Edf Annotations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test annotations in the exported EDF file.

All annotations should be preserved and onset corrected.

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
# Fixtures: tmp_path, tmin
```

## Step-by-Step Guide

### Step 1: 'Test annotations in the exported EDF file.\n\n    All annotations should be preserved and onset corrected.\n    '

```python
'Test annotations in the exported EDF file.\n\n    All annotations should be preserved and onset corrected.\n    '
```

**Verification:**
```python
assert raw.first_time == tmin
```

### Step 2: Assign raw = _create_raw_for_edf_tests(...)

```python
raw = _create_raw_for_edf_tests()
```

**Verification:**
```python
assert raw_read.first_time == 0
```

### Step 3: Assign annotations = Annotations(...)

```python
annotations = Annotations(onset=[0.01, 0.05, 0.9, 1.05], duration=[0, 1, 0, 0], description=['test1', 'test2', 'test3', 'test4'], ch_names=[['0'], ['0', '1'], [], ['1']])
```

**Verification:**
```python
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
```

### Step 4: Call raw.set_annotations()

```python
raw.set_annotations(annotations)
```

**Verification:**
```python
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
```

### Step 5: Call raw.crop()

```python
raw.crop(tmin)
```

**Verification:**
```python
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
```

### Step 6: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.edf'
```

**Verification:**
```python
assert_array_equal(raw.annotations.ch_names[valid_annot], raw_read.annotations.ch_names)
```

### Step 7: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, preload=True)
```

**Verification:**
```python
assert raw_read.first_time == 0
```

### Step 8: Assign bad_annot = value

```python
bad_annot = raw_read.annotations.description == 'BAD_ACQ_SKIP'
```

### Step 9: Assign valid_annot = value

```python
valid_annot = raw.annotations.onset >= tmin
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.ch_names[valid_annot], raw_read.annotations.ch_names)
```

### Step 14: Assign expectation = nullcontext(...)

```python
expectation = nullcontext()
```

### Step 15: Assign expectation = pytest.warns(...)

```python
expectation = pytest.warns(RuntimeWarning, match='EDF format requires equal-length data blocks')
```

### Step 16: Call raw.export()

```python
raw.export(temp_fname)
```

### Step 17: Call raw_read.annotations.delete()

```python
raw_read.annotations.delete(bad_annot)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, tmin

# Workflow
'Test annotations in the exported EDF file.\n\n    All annotations should be preserved and onset corrected.\n    '
raw = _create_raw_for_edf_tests()
annotations = Annotations(onset=[0.01, 0.05, 0.9, 1.05], duration=[0, 1, 0, 0], description=['test1', 'test2', 'test3', 'test4'], ch_names=[['0'], ['0', '1'], [], ['1']])
raw.set_annotations(annotations)
raw.crop(tmin)
assert raw.first_time == tmin
if raw.n_times % raw.info['sfreq'] == 0:
    expectation = nullcontext()
else:
    expectation = pytest.warns(RuntimeWarning, match='EDF format requires equal-length data blocks')
temp_fname = tmp_path / 'test.edf'
with expectation:
    raw.export(temp_fname)
raw_read = read_raw_edf(temp_fname, preload=True)
assert raw_read.first_time == 0
bad_annot = raw_read.annotations.description == 'BAD_ACQ_SKIP'
if bad_annot.any():
    raw_read.annotations.delete(bad_annot)
valid_annot = raw.annotations.onset >= tmin
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
assert_array_equal(raw.annotations.ch_names[valid_annot], raw_read.annotations.ch_names)
```

## Next Steps


---

*Source: test_export.py:308 | Complexity: Advanced | Last updated: 2026-05-18*