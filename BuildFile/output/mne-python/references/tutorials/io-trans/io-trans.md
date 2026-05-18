# How To: Io Trans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading and writing of trans files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.transforms`
- `mne.transforms`
- `dipy.align`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading and writing of trans files.'

```python
'Test reading and writing of trans files.'
```

**Verification:**
```python
assert fname1 == got_fname
```

### Step 2: Call os.mkdir()

```python
os.mkdir(tmp_path / 'sample')
```

**Verification:**
```python
assert trans0 == trans1
```

### Step 3: Call pytest.raises()

```python
pytest.raises(RuntimeError, _find_trans, trans='auto', subject='sample', subjects_dir=tmp_path)
```

### Step 4: Assign trans0 = read_trans(...)

```python
trans0 = read_trans(fname)
```

### Step 5: Assign fname1 = value

```python
fname1 = tmp_path / 'sample' / 'test-trans.fif'
```

### Step 6: Call trans0.save()

```python
trans0.save(fname1)
```

### Step 7: Assign unknown = _find_trans(...)

```python
trans1, got_fname = _find_trans(trans='auto', subject='sample', subjects_dir=tmp_path)
```

**Verification:**
```python
assert fname1 == got_fname
```

### Step 8: Assign trans1 = read_trans(...)

```python
trans1 = read_trans(fname1)
```

**Verification:**
```python
assert trans0 == trans1
```

### Step 9: Call pytest.raises()

```python
pytest.raises(OSError, read_trans, fname_eve)
```

### Step 10: Assign fname2 = value

```python
fname2 = tmp_path / 'trans-test-bad-name.fif'
```

### Step 11: Call write_trans()

```python
write_trans(fname2, trans0)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading and writing of trans files.'
os.mkdir(tmp_path / 'sample')
pytest.raises(RuntimeError, _find_trans, trans='auto', subject='sample', subjects_dir=tmp_path)
trans0 = read_trans(fname)
fname1 = tmp_path / 'sample' / 'test-trans.fif'
trans0.save(fname1)
trans1, got_fname = _find_trans(trans='auto', subject='sample', subjects_dir=tmp_path)
assert fname1 == got_fname
trans1 = read_trans(fname1)
assert trans0 == trans1
pytest.raises(OSError, read_trans, fname_eve)
fname2 = tmp_path / 'trans-test-bad-name.fif'
with pytest.warns(RuntimeWarning, match='-trans.fif'):
    write_trans(fname2, trans0)
```

## Next Steps


---

*Source: test_transforms.py:104 | Complexity: Advanced | Last updated: 2026-05-18*