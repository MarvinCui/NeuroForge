# How To: Write Complex File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write complex file

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

### Step 1: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_point=DATA['data_per_point'], affine_to_rasmm=np.eye(4))
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 2: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 3: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 4: Call trk.save()

```python
trk.save(trk_file)
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 5: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['complex_trk_fname'], 'rb').read()
```

### Step 6: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file, lazy_load=False)
```

### Step 7: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 8: Assign data_per_streamline = value

```python
data_per_streamline = DATA['data_per_streamline']
```

### Step 9: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
```

### Step 10: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 11: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 12: Call trk.save()

```python
trk.save(trk_file)
```

### Step 13: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 14: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file, lazy_load=False)
```

### Step 15: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 16: Assign data_per_streamline = value

```python
data_per_streamline = DATA['data_per_streamline']
```

### Step 17: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_point=DATA['data_per_point'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
```

### Step 18: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 19: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 20: Call trk.save()

```python
trk.save(trk_file)
```

### Step 21: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 22: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file, lazy_load=False)
```

### Step 23: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 24: Assign new_trk_orig = TrkFile.load(...)

```python
new_trk_orig = TrkFile.load(DATA['complex_trk_fname'])
```

### Step 25: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
```

### Step 26: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert trk_file.read() == open(DATA['complex_trk_fname'], 'rb').read()
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(DATA['streamlines'], data_per_point=DATA['data_per_point'], affine_to_rasmm=np.eye(4))
trk_file = BytesIO()
trk = TrkFile(tractogram)
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file, lazy_load=False)
assert_tractogram_equal(new_trk.tractogram, tractogram)
data_per_streamline = DATA['data_per_streamline']
tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
trk = TrkFile(tractogram)
trk_file = BytesIO()
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file, lazy_load=False)
assert_tractogram_equal(new_trk.tractogram, tractogram)
data_per_streamline = DATA['data_per_streamline']
tractogram = Tractogram(DATA['streamlines'], data_per_point=DATA['data_per_point'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
trk_file = BytesIO()
trk = TrkFile(tractogram)
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file, lazy_load=False)
assert_tractogram_equal(new_trk.tractogram, tractogram)
new_trk_orig = TrkFile.load(DATA['complex_trk_fname'])
assert_tractogram_equal(new_trk.tractogram, new_trk_orig.tractogram)
trk_file.seek(0, os.SEEK_SET)
assert trk_file.read() == open(DATA['complex_trk_fname'], 'rb').read()
```

## Next Steps


---

*Source: test_trk.py:252 | Complexity: Advanced | Last updated: 2026-05-18*