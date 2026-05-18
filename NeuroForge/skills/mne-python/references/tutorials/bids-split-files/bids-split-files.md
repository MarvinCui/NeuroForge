# How To: Bids Split Files

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that BIDS split files are written safely.

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

### Step 1: 'Test that BIDS split files are written safely.'

```python
'Test that BIDS split files are written safely.'
```

**Verification:**
```python
assert not want_path.is_file()
```

### Step 2: Assign mne_bids = pytest.importorskip(...)

```python
mne_bids = pytest.importorskip('mne_bids')
```

**Verification:**
```python
assert want_path.is_file(), want_path
```

### Step 3: Assign bids_path = mne_bids.BIDSPath(...)

```python
bids_path = mne_bids.BIDSPath(root=tmp_path, subject='01', datatype='meg', split='01', suffix='raw', extension='.fif', check=False)
```

### Step 4: Call unknown.mkdir()

```python
(tmp_path / 'sub-01' / 'meg').mkdir(parents=True)
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(test_fif_fname)
```

### Step 6: Assign save_kwargs = dict(...)

```python
save_kwargs = dict(buffer_size_sec=1.0, split_size='10MB', split_naming='bids', verbose=True)
```

### Step 7: Assign bids_path.split = None

```python
bids_path.split = None
```

### Step 8: Assign want_paths = value

```python
want_paths = [Path(bids_path.copy().update(split=f'{ii:02d}').fpath) for ii in range(1, 3)]
```

### Step 9: Call raw.save()

```python
raw.save(bids_path, **save_kwargs)
```

### Step 10: Call raw.save()

```python
raw.save(bids_path, **save_kwargs)
```

**Verification:**
```python
assert not want_path.is_file()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that BIDS split files are written safely.'
mne_bids = pytest.importorskip('mne_bids')
bids_path = mne_bids.BIDSPath(root=tmp_path, subject='01', datatype='meg', split='01', suffix='raw', extension='.fif', check=False)
(tmp_path / 'sub-01' / 'meg').mkdir(parents=True)
raw = read_raw_fif(test_fif_fname)
save_kwargs = dict(buffer_size_sec=1.0, split_size='10MB', split_naming='bids', verbose=True)
with pytest.raises(ValueError, match='Passing a BIDSPath'):
    raw.save(bids_path, **save_kwargs)
bids_path.split = None
want_paths = [Path(bids_path.copy().update(split=f'{ii:02d}').fpath) for ii in range(1, 3)]
for want_path in want_paths:
    assert not want_path.is_file()
raw.save(bids_path, **save_kwargs)
for want_path in want_paths:
    assert want_path.is_file(), want_path
```

## Next Steps


---

*Source: test_raw_fiff.py:705 | Complexity: Advanced | Last updated: 2026-05-18*