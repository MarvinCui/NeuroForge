# How To: Load Bad Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading/writing of bad channels.

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

### Step 1: 'Test reading/writing of bad channels.'

```python
'Test reading/writing of bad channels.'
```

**Verification:**
```python
assert_array_equal(raw.info['bads'], [])
```

### Step 2: Assign raw_marked = read_raw_fif(...)

```python
raw_marked = read_raw_fif(fif_bad_marked_fname)
```

**Verification:**
```python
assert correct_bads == raw_new.info['bads']
```

### Step 3: Assign correct_bads = value

```python
correct_bads = raw_marked.info['bads']
```

**Verification:**
```python
assert correct_bads == raw_new.info['bads']
```

### Step 4: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(test_fif_fname)
```

**Verification:**
```python
assert raw_new.info['bads'] == []
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(raw.info['bads'], [])
```

### Step 6: Call raw.load_bad_channels()

```python
raw.load_bad_channels(bad_file_works)
```

### Step 7: Call raw.save()

```python
raw.save(tmp_path / 'foo_raw.fif')
```

### Step 8: Assign raw_new = read_raw_fif(...)

```python
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
```

**Verification:**
```python
assert correct_bads == raw_new.info['bads']
```

### Step 9: Assign unknown = value

```python
raw.info['bads'] = []
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, raw.load_bad_channels, bad_file_wrong)
```

### Step 11: Call raw.save()

```python
raw.save(tmp_path / 'foo_raw.fif', overwrite=True)
```

### Step 12: Assign raw_new = read_raw_fif(...)

```python
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
```

**Verification:**
```python
assert correct_bads == raw_new.info['bads']
```

### Step 13: Call raw.load_bad_channels()

```python
raw.load_bad_channels(None)
```

### Step 14: Call raw.save()

```python
raw.save(tmp_path / 'foo_raw.fif', overwrite=True)
```

### Step 15: Assign raw_new = read_raw_fif(...)

```python
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
```

**Verification:**
```python
assert raw_new.info['bads'] == []
```

### Step 16: Call raw.load_bad_channels()

```python
raw.load_bad_channels(bad_file_wrong, force=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading/writing of bad channels.'
raw_marked = read_raw_fif(fif_bad_marked_fname)
correct_bads = raw_marked.info['bads']
raw = read_raw_fif(test_fif_fname)
assert_array_equal(raw.info['bads'], [])
raw.load_bad_channels(bad_file_works)
raw.save(tmp_path / 'foo_raw.fif')
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
assert correct_bads == raw_new.info['bads']
raw.info['bads'] = []
pytest.raises(ValueError, raw.load_bad_channels, bad_file_wrong)
with pytest.warns(RuntimeWarning, match='1 bad channel'):
    raw.load_bad_channels(bad_file_wrong, force=True)
raw.save(tmp_path / 'foo_raw.fif', overwrite=True)
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
assert correct_bads == raw_new.info['bads']
raw.load_bad_channels(None)
raw.save(tmp_path / 'foo_raw.fif', overwrite=True)
raw_new = read_raw_fif(tmp_path / 'foo_raw.fif')
assert raw_new.info['bads'] == []
```

## Next Steps


---

*Source: test_raw_fiff.py:759 | Complexity: Advanced | Last updated: 2026-05-18*