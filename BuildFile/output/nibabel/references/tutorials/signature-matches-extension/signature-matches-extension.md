# How To: Signature Matches Extension

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test signature matches extension

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `shutil`
- `os.path`
- `os.path`
- `tempfile`
- `numpy`
- `_compression`
- `filebasedimages`
- `loadsave`
- `openers`
- `optpkg`
- `testing`
- `tmpdirs`
- `pytest`
- `numpy.testing`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign gz_signature = b'\x1f\x8b'

```python
gz_signature = b'\x1f\x8b'
```

**Verification:**
```python
assert matches
```

### Step 2: Assign good_file = value

```python
good_file = tmp_path / 'good.gz'
```

**Verification:**
```python
assert msg == ''
```

### Step 3: Call good_file.write_bytes()

```python
good_file.write_bytes(gz_signature)
```

**Verification:**
```python
assert not matches
```

### Step 4: Assign bad_file = value

```python
bad_file = tmp_path / 'bad.gz'
```

**Verification:**
```python
assert msg.startswith('Could not read')
```

### Step 5: Call bad_file.write_bytes()

```python
bad_file.write_bytes(b'bad')
```

**Verification:**
```python
assert not matches
```

### Step 6: Assign unknown = _signature_matches_extension(...)

```python
matches, msg = _signature_matches_extension(tmp_path / 'uncompressed.nii')
```

**Verification:**
```python
assert 'is not a' in msg
```

### Step 7: Assign unknown = _signature_matches_extension(...)

```python
matches, msg = _signature_matches_extension(tmp_path / 'missing.gz')
```

**Verification:**
```python
assert matches
```

### Step 8: Assign unknown = _signature_matches_extension(...)

```python
matches, msg = _signature_matches_extension(bad_file)
```

**Verification:**
```python
assert msg == ''
```

### Step 9: Assign unknown = _signature_matches_extension(...)

```python
matches, msg = _signature_matches_extension(good_file)
```

**Verification:**
```python
assert matches
```

### Step 10: Assign unknown = _signature_matches_extension(...)

```python
matches, msg = _signature_matches_extension(tmp_path / 'missing.nii')
```

**Verification:**
```python
assert msg == ''
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
gz_signature = b'\x1f\x8b'
good_file = tmp_path / 'good.gz'
good_file.write_bytes(gz_signature)
bad_file = tmp_path / 'bad.gz'
bad_file.write_bytes(b'bad')
matches, msg = _signature_matches_extension(tmp_path / 'uncompressed.nii')
assert matches
assert msg == ''
matches, msg = _signature_matches_extension(tmp_path / 'missing.gz')
assert not matches
assert msg.startswith('Could not read')
matches, msg = _signature_matches_extension(bad_file)
assert not matches
assert 'is not a' in msg
matches, msg = _signature_matches_extension(good_file)
assert matches
assert msg == ''
matches, msg = _signature_matches_extension(tmp_path / 'missing.nii')
assert matches
assert msg == ''
```

## Next Steps


---

*Source: test_loadsave.py:107 | Complexity: Advanced | Last updated: 2026-05-18*