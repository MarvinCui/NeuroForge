# How To: Opener Gzip Type

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, unittest, workflow, integration

## Overview

Workflow: test Opener gzip type

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `hashlib`
- `os`
- `time`
- `unittest`
- `gzip`
- `io`
- `unittest`
- `pytest`
- `packaging.version`
- `_compression`
- `openers`
- `tmpdirs`
- `indexed_gzip`
- `_compression`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign data = b'this is some test data'

```python
data = b'this is some test data'
```

**Verification:**
```python
assert isinstance(opener.fobj, expected)
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'test.gz'
```

### Step 3: Assign tests = value

```python
tests = [(False, {'mode': 'rb', 'keep_open': True}, GzipFile), (False, {'mode': 'rb', 'keep_open': False}, GzipFile), (False, {'mode': 'wb', 'keep_open': True}, GzipFile), (False, {'mode': 'wb', 'keep_open': False}, GzipFile), (True, {'mode': 'rb', 'keep_open': True}, MockIndexedGzipFile), (True, {'mode': 'rb', 'keep_open': False}, MockIndexedGzipFile), (True, {'mode': 'wb', 'keep_open': True}, GzipFile), (True, {'mode': 'wb', 'keep_open': False}, GzipFile)]
```

### Step 4: Call f.write()

```python
f.write(data)
```

### Step 5: Assign unknown = test

```python
igzip_present, kwargs, expected = test
```

### Step 6: Assign opener = Opener(...)

```python
opener = Opener(fname, **kwargs)
```

**Verification:**
```python
assert isinstance(opener.fobj, expected)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
data = b'this is some test data'
fname = tmp_path / 'test.gz'
with GzipFile(fname, mode='wb') as f:
    f.write(data)
tests = [(False, {'mode': 'rb', 'keep_open': True}, GzipFile), (False, {'mode': 'rb', 'keep_open': False}, GzipFile), (False, {'mode': 'wb', 'keep_open': True}, GzipFile), (False, {'mode': 'wb', 'keep_open': False}, GzipFile), (True, {'mode': 'rb', 'keep_open': True}, MockIndexedGzipFile), (True, {'mode': 'rb', 'keep_open': False}, MockIndexedGzipFile), (True, {'mode': 'wb', 'keep_open': True}, GzipFile), (True, {'mode': 'wb', 'keep_open': False}, GzipFile)]
for test in tests:
    igzip_present, kwargs, expected = test
    with patch_indexed_gzip(igzip_present):
        opener = Opener(fname, **kwargs)
        assert isinstance(opener.fobj, expected)
        del opener
```

## Next Steps


---

*Source: test_openers.py:130 | Complexity: Intermediate | Last updated: 2026-05-18*