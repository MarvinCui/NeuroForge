# How To: Hashfunc

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test md5/sha1 hash calculations.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test md5/sha1 hash calculations.'

```python
'Test md5/sha1 hash calculations.'
```

**Verification:**
```python
assert hash1 == hash1_
```

### Step 2: Assign fname1 = value

```python
fname1 = tmp_path / 'foo'
```

**Verification:**
```python
assert hash2 == hash2_
```

### Step 3: Assign fname2 = value

```python
fname2 = tmp_path / 'bar'
```

**Verification:**
```python
assert hash1 != hash2
```

### Step 4: Call fid.write()

```python
fid.write(b'abcd')
```

### Step 5: Call fid.write()

```python
fid.write(b'efgh')
```

### Step 6: Assign hash1 = hashfunc(...)

```python
hash1 = hashfunc(fname1, hash_type=hash_type)
```

### Step 7: Assign hash1_ = hashfunc(...)

```python
hash1_ = hashfunc(fname1, 1, hash_type=hash_type)
```

### Step 8: Assign hash2 = hashfunc(...)

```python
hash2 = hashfunc(fname2, hash_type=hash_type)
```

### Step 9: Assign hash2_ = hashfunc(...)

```python
hash2_ = hashfunc(fname2, 1024, hash_type=hash_type)
```

**Verification:**
```python
assert hash1 == hash1_
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test md5/sha1 hash calculations.'
fname1 = tmp_path / 'foo'
fname2 = tmp_path / 'bar'
with open(fname1, 'wb') as fid:
    fid.write(b'abcd')
with open(fname2, 'wb') as fid:
    fid.write(b'efgh')
for hash_type in ('md5', 'sha1'):
    hash1 = hashfunc(fname1, hash_type=hash_type)
    hash1_ = hashfunc(fname1, 1, hash_type=hash_type)
    hash2 = hashfunc(fname2, hash_type=hash_type)
    hash2_ = hashfunc(fname2, 1024, hash_type=hash_type)
    assert hash1 == hash1_
    assert hash2 == hash2_
    assert hash1 != hash2
```

## Next Steps


---

*Source: test_numerics.py:78 | Complexity: Advanced | Last updated: 2026-05-18*