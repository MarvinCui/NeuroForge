# How To: Mlist

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test mlist

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `numpy`
- `py3k`
- `volumeutils`
- `ecat`
- `unittest`
- `nose.tools`
- `numpy.testing`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign fid = open(...)

```python
fid = open(self.example_file, 'rb')
```

**Verification:**
```python
assert_true(mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31)
```

### Step 2: Assign hdr = self.header_class.from_fileobj(...)

```python
hdr = self.header_class.from_fileobj(fid)
```

**Verification:**
```python
assert_true(mlist.get_frame_order()[0][0] == 0)
```

### Step 3: Assign mlist = self.mlist_class(...)

```python
mlist = self.mlist_class(fid, hdr)
```

**Verification:**
```python
assert_true(mlist.get_frame_order()[0][1] == 16842758.0)
```

### Step 4: Call fid.seek()

```python
fid.seek(0)
```

**Verification:**
```python
assert_true(badordermlist.get_frame_order()[0][0] == 1)
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

### Step 11: Call assert_true()

```python
assert_true(mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31)
```

### Step 12: Call assert_true()

```python
assert_true(mlist.get_frame_order()[0][0] == 0)
```

### Step 13: Call assert_true()

```python
assert_true(mlist.get_frame_order()[0][1] == 16842758.0)
```

### Step 14: Assign badordermlist = mlist

```python
badordermlist = mlist
```

### Step 15: Assign badordermlist._mlist = np.array(...)

```python
badordermlist._mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
```

### Step 16: Call assert_true()

```python
assert_true(badordermlist.get_frame_order()[0][0] == 1)
```


## Complete Example

```python
# Workflow
fid = open(self.example_file, 'rb')
hdr = self.header_class.from_fileobj(fid)
mlist = self.mlist_class(fid, hdr)
fid.seek(0)
fid.seek(512)
dat = fid.read(128 * 32)
dt = np.dtype([('matlist', np.int32)])
dt = dt.newbyteorder('>')
mats = np.recarray(shape=(32, 4), dtype=dt, buf=dat)
fid.close()
assert_true(mats['matlist'][0, 0] + mats['matlist'][0, 3] == 31)
assert_true(mlist.get_frame_order()[0][0] == 0)
assert_true(mlist.get_frame_order()[0][1] == 16842758.0)
badordermlist = mlist
badordermlist._mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
assert_true(badordermlist.get_frame_order()[0][0] == 1)
```

## Next Steps


---

*Source: test_ecat.py:95 | Complexity: Advanced | Last updated: 2026-05-18*