# How To: Mlist

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test mlist

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `ecat`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`


## Step-by-Step Guide

### Step 1: Assign fid = open(...)

```python
fid = open(self.example_file, 'rb')
```

**Verification:**
```python
assert mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31
```

### Step 2: Assign hdr = self.header_class.from_fileobj(...)

```python
hdr = self.header_class.from_fileobj(fid)
```

**Verification:**
```python
assert get_frame_order(mlist)[0][0] == 0
```

### Step 3: Assign mlist = read_mlist(...)

```python
mlist = read_mlist(fid, hdr.endianness)
```

**Verification:**
```python
assert get_frame_order(mlist)[0][1] == 16842758.0
```

### Step 4: Call fid.seek()

```python
fid.seek(0)
```

**Verification:**
```python
assert get_frame_order(badordermlist)[0][0] == 1
```

### Step 5: Call fid.seek()

```python
fid.seek(512)
```

### Step 6: Assign dat = fid.read(...)

```python
dat = fid.read(128 * 32)
```

### Step 7: Assign dt = np.dtype(...)

```python
dt = np.dtype([('matlist', np.int32)])
```

### Step 8: Assign dt = dt.newbyteorder(...)

```python
dt = dt.newbyteorder('>')
```

### Step 9: Assign mats = np.recarray(...)

```python
mats = np.recarray(shape=(32, 4), dtype=dt, buf=dat)
```

### Step 10: Call fid.close()

```python
fid.close()
```

**Verification:**
```python
assert mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31
```

### Step 11: Assign badordermlist = np.array(...)

```python
badordermlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
```

**Verification:**
```python
assert get_frame_order(badordermlist)[0][0] == 1
```


## Complete Example

```python
# Workflow
fid = open(self.example_file, 'rb')
hdr = self.header_class.from_fileobj(fid)
mlist = read_mlist(fid, hdr.endianness)
fid.seek(0)
fid.seek(512)
dat = fid.read(128 * 32)
dt = np.dtype([('matlist', np.int32)])
dt = dt.newbyteorder('>')
mats = np.recarray(shape=(32, 4), dtype=dt, buf=dat)
fid.close()
assert mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31
assert get_frame_order(mlist)[0][0] == 0
assert get_frame_order(mlist)[0][1] == 16842758.0
badordermlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
with suppress_warnings():
    assert get_frame_order(badordermlist)[0][0] == 1
```

## Next Steps


---

*Source: test_ecat.py:87 | Complexity: Advanced | Last updated: 2026-05-18*