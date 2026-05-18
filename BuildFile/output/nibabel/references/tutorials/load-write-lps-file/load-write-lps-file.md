# How To: Load Write Lps File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load write LPS file

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

### Step 1: Assign trk_RAS = TrkFile.load(...)

```python
trk_RAS = TrkFile.load(DATA['standard_trk_fname'], lazy_load=False)
```

**Verification:**
```python
assert_tractogram_equal(trk_LPS.tractogram, trk_RAS.tractogram)
```

### Step 2: Assign trk_LPS = TrkFile.load(...)

```python
trk_LPS = TrkFile.load(DATA['standard_LPS_trk_fname'], lazy_load=False)
```

**Verification:**
```python
assert_arr_dict_equal(new_trk.header, trk.header)
```

### Step 3: Call assert_tractogram_equal()

```python
assert_tractogram_equal(trk_LPS.tractogram, trk_RAS.tractogram)
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
```

### Step 4: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 5: Assign trk = TrkFile(...)

```python
trk = TrkFile(trk_LPS.tractogram, trk_LPS.header)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
```

### Step 6: Call trk.save()

```python
trk.save(trk_file)
```

**Verification:**
```python
assert_arr_dict_equal(new_trk.header, trk_LPS.header)
```

### Step 7: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
```

### Step 8: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file)
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 9: Call assert_arr_dict_equal()

```python
assert_arr_dict_equal(new_trk.header, trk.header)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
```

### Step 10: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
```

### Step 11: Assign new_trk_orig = TrkFile.load(...)

```python
new_trk_orig = TrkFile.load(DATA['standard_LPS_trk_fname'])
```

### Step 12: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 13: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
```

### Step 14: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 15: Assign header = copy.deepcopy(...)

```python
header = copy.deepcopy(trk_LPS.header)
```

### Step 16: Assign unknown = b''

```python
header[Field.VOXEL_ORDER] = b''
```

### Step 17: Assign trk = TrkFile(...)

```python
trk = TrkFile(trk_LPS.tractogram, header)
```

### Step 18: Call trk.save()

```python
trk.save(trk_file)
```

### Step 19: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 20: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file)
```

### Step 21: Call assert_arr_dict_equal()

```python
assert_arr_dict_equal(new_trk.header, trk_LPS.header)
```

### Step 22: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
```

### Step 23: Assign new_trk_orig = TrkFile.load(...)

```python
new_trk_orig = TrkFile.load(DATA['standard_LPS_trk_fname'])
```

### Step 24: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 25: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
```


## Complete Example

```python
# Workflow
trk_RAS = TrkFile.load(DATA['standard_trk_fname'], lazy_load=False)
trk_LPS = TrkFile.load(DATA['standard_LPS_trk_fname'], lazy_load=False)
assert_tractogram_equal(trk_LPS.tractogram, trk_RAS.tractogram)
trk_file = BytesIO()
trk = TrkFile(trk_LPS.tractogram, trk_LPS.header)
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file)
assert_arr_dict_equal(new_trk.header, trk.header)
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
new_trk_orig = TrkFile.load(DATA['standard_LPS_trk_fname'])
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
trk_file.seek(0, os.SEEK_SET)
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
trk_file = BytesIO()
header = copy.deepcopy(trk_LPS.header)
header[Field.VOXEL_ORDER] = b''
trk = TrkFile(trk_LPS.tractogram, header)
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file)
assert_arr_dict_equal(new_trk.header, trk_LPS.header)
assert_tractogram_equal(new_trk.tractogram, trk.tractogram)
new_trk_orig = TrkFile.load(DATA['standard_LPS_trk_fname'])
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
trk_file.seek(0, os.SEEK_SET)
assert trk_file.read() == open(DATA['standard_LPS_trk_fname'], 'rb').read()
```

## Next Steps


---

*Source: test_trk.py:317 | Complexity: Advanced | Last updated: 2026-05-18*