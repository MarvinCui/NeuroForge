# How To: Header Read Restore

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test header read restore

## Prerequisites

**Required Modules:**
- `copy`
- `os`
- `sys`
- `unittest`
- `io`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `header`
- `tractogram`
- `tractogram_file`
- `trk`
- `test_tractogram`


## Step-by-Step Guide

### Step 1: Assign trk_fname = value

```python
trk_fname = DATA['simple_trk_fname']
```

**Verification:**
```python
assert_arr_dict_equal(TrkFile._read_header(bio), hdr_from_fname)
```

### Step 2: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert bio.tell() == hdr_pos
```

### Step 3: Call bio.write()

```python
bio.write(b'Along my very merry way')
```

### Step 4: Assign hdr_pos = bio.tell(...)

```python
hdr_pos = bio.tell()
```

### Step 5: Assign hdr_from_fname = TrkFile._read_header(...)

```python
hdr_from_fname = TrkFile._read_header(trk_fname)
```

### Step 6: Call bio.seek()

```python
bio.seek(hdr_pos)
```

### Step 7: Call assert_arr_dict_equal()

```python
assert_arr_dict_equal(TrkFile._read_header(bio), hdr_from_fname)
```

**Verification:**
```python
assert bio.tell() == hdr_pos
```

### Step 8: Call bio.write()

```python
bio.write(fobj.read())
```


## Complete Example

```python
# Workflow
trk_fname = DATA['simple_trk_fname']
bio = BytesIO()
bio.write(b'Along my very merry way')
hdr_pos = bio.tell()
hdr_from_fname = TrkFile._read_header(trk_fname)
with open(trk_fname, 'rb') as fobj:
    bio.write(fobj.read())
bio.seek(hdr_pos)
hdr_from_fname['_offset_data'] += hdr_pos
assert_arr_dict_equal(TrkFile._read_header(bio), hdr_from_fname)
assert bio.tell() == hdr_pos
```

## Next Steps


---

*Source: test_trk.py:503 | Complexity: Advanced | Last updated: 2026-05-18*