# How To: Hash Raw

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test hashing raw objects.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test hashing raw objects.'

```python
'Test hashing raw objects.'
```

**Verification:**
```python
assert raw_size < raw_load_size
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fif_fname)
```

**Verification:**
```python
assert hash(raw) == hash(raw_2)
```

### Step 3: Call pytest.raises()

```python
pytest.raises(RuntimeError, raw.__hash__)
```

**Verification:**
```python
assert pickle.dumps(raw) == pickle.dumps(raw_2)
```

### Step 4: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(fif_fname).crop(0, 0.5)
```

**Verification:**
```python
assert hash(raw) != hash(raw_2)
```

### Step 5: Assign raw_size = value

```python
raw_size = raw._size
```

### Step 6: Call raw.load_data()

```python
raw.load_data()
```

### Step 7: Assign raw_load_size = value

```python
raw_load_size = raw._size
```

**Verification:**
```python
assert raw_size < raw_load_size
```

### Step 8: Assign raw_2 = read_raw_fif.crop(...)

```python
raw_2 = read_raw_fif(fif_fname).crop(0, 0.5)
```

### Step 9: Call raw_2.load_data()

```python
raw_2.load_data()
```

**Verification:**
```python
assert hash(raw) == hash(raw_2)
```


## Complete Example

```python
# Workflow
'Test hashing raw objects.'
raw = read_raw_fif(fif_fname)
pytest.raises(RuntimeError, raw.__hash__)
raw = read_raw_fif(fif_fname).crop(0, 0.5)
raw_size = raw._size
raw.load_data()
raw_load_size = raw._size
assert raw_size < raw_load_size
raw_2 = read_raw_fif(fif_fname).crop(0, 0.5)
raw_2.load_data()
assert hash(raw) == hash(raw_2)
assert pickle.dumps(raw) == pickle.dumps(raw_2)
raw_2._data[0, 0] -= 1
assert hash(raw) != hash(raw_2)
```

## Next Steps


---

*Source: test_raw_fiff.py:161 | Complexity: Advanced | Last updated: 2026-05-18*