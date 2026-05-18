# How To: Split Numbers

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test handling of split files using numbers instead of names.

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
# Fixtures: tmp_path, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test handling of split files using numbers instead of names.'

```python
'Test handling of split files using numbers instead of names.'
```

**Verification:**
```python
assert dashes_fname.is_file()
```

### Step 2: Call monkeypatch.setattr()

```python
monkeypatch.setattr(base, 'write_string', _no_write_file_name)
```

**Verification:**
```python
assert next_fname.is_file()
```

### Step 3: Assign raw = read_raw_fif.pick(...)

```python
raw = read_raw_fif(test_fif_fname).pick('eeg')
```

**Verification:**
```python
assert_allclose(raw.times, raw_read.times)
```

### Step 4: Assign dashes_fname = value

```python
dashes_fname = tmp_path / 'sub-1_ses-2_task-3_raw.fif'
```

**Verification:**
```python
assert_allclose(raw.get_data(), raw_read.get_data(), atol=1e-16)
```

### Step 5: Call raw.save()

```python
raw.save(dashes_fname, split_size='5MB', buffer_size_sec=1.0)
```

**Verification:**
```python
assert dashes_fname.is_file()
```

### Step 6: Assign next_fname = Path(...)

```python
next_fname = Path(str(dashes_fname)[:-4] + '-1.fif')
```

**Verification:**
```python
assert next_fname.is_file()
```

### Step 7: Assign raw_read = read_raw_fif(...)

```python
raw_read = read_raw_fif(dashes_fname)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(raw.times, raw_read.times)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw.get_data(), raw_read.get_data(), atol=1e-16)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, monkeypatch

# Workflow
'Test handling of split files using numbers instead of names.'
monkeypatch.setattr(base, 'write_string', _no_write_file_name)
raw = read_raw_fif(test_fif_fname).pick('eeg')
dashes_fname = tmp_path / 'sub-1_ses-2_task-3_raw.fif'
raw.save(dashes_fname, split_size='5MB', buffer_size_sec=1.0)
assert dashes_fname.is_file()
next_fname = Path(str(dashes_fname)[:-4] + '-1.fif')
assert next_fname.is_file()
raw_read = read_raw_fif(dashes_fname)
assert_allclose(raw.times, raw_read.times)
assert_allclose(raw.get_data(), raw_read.get_data(), atol=1e-16)
```

## Next Steps


---

*Source: test_raw_fiff.py:744 | Complexity: Advanced | Last updated: 2026-05-18*