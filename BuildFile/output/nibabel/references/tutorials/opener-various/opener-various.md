# How To: Opener Various

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test Opener various

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign message = b'Oh what a giveaway'

```python
message = b'Oh what a giveaway'
```

**Verification:**
```python
assert fobj.tell() == len(message)
```

### Step 2: Assign bz2_fileno = hasattr(...)

```python
bz2_fileno = hasattr(BZ2File, 'fileno')
```

**Verification:**
```python
assert message == message_back
```

### Step 3: Assign sobj = BytesIO(...)

```python
sobj = BytesIO()
```

**Verification:**
```python
assert fobj.fileno() != 0
```

### Step 4: Assign files_to_test = value

```python
files_to_test = ['test.txt', 'test.txt.gz', 'test.txt.bz2', sobj]
```

### Step 5: Call fobj.write()

```python
fobj.write(message)
```

**Verification:**
```python
assert fobj.tell() == len(message)
```

### Step 6: Call input.seek()

```python
input.seek(0)
```

### Step 7: Assign message_back = fobj.read(...)

```python
message_back = fobj.read()
```

**Verification:**
```python
assert message == message_back
```

### Step 8: Call fobj.fileno()

```python
fobj.fileno()
```

### Step 9: Call fobj.fileno()

```python
fobj.fileno()
```

**Verification:**
```python
assert fobj.fileno() != 0
```

### Step 10: Call fobj.fileno()

```python
fobj.fileno()
```


## Complete Example

```python
# Workflow
message = b'Oh what a giveaway'
bz2_fileno = hasattr(BZ2File, 'fileno')
if HAVE_INDEXED_GZIP:
    import indexed_gzip as igzip
with InTemporaryDirectory():
    sobj = BytesIO()
    files_to_test = ['test.txt', 'test.txt.gz', 'test.txt.bz2', sobj]
    if HAVE_ZSTD:
        files_to_test += ['test.txt.zst']
    for input in files_to_test:
        with Opener(input, 'wb') as fobj:
            fobj.write(message)
            assert fobj.tell() == len(message)
        if input == sobj:
            input.seek(0)
        with Opener(input, 'rb') as fobj:
            message_back = fobj.read()
            assert message == message_back
            if input == sobj:
                with pytest.raises(UnsupportedOperation):
                    fobj.fileno()
            elif input.endswith('.bz2') and (not bz2_fileno):
                with pytest.raises(AttributeError):
                    fobj.fileno()
            elif input.endswith('gz') and HAVE_INDEXED_GZIP and (Version(igzip.__version__) >= Version('0.7.0')):
                with pytest.raises(igzip.NoHandleError):
                    fobj.fileno()
            else:
                assert fobj.fileno() != 0
```

## Next Steps


---

*Source: test_openers.py:68 | Complexity: Advanced | Last updated: 2026-05-18*