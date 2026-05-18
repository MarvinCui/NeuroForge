# How To: Write Empty File

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write empty file

## Prerequisites

**Required Modules:**
- `os`
- `unittest`
- `io`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `array_sequence`
- `tck`
- `tractogram`
- `tractogram_file`
- `test_tractogram`


## Step-by-Step Guide

### Step 1: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(affine_to_rasmm=np.eye(4))
```

**Verification:**
```python
assert_tractogram_equal(new_tck.tractogram, tractogram)
```

### Step 2: Assign tck_file = BytesIO(...)

```python
tck_file = BytesIO()
```

**Verification:**
```python
assert_tractogram_equal(new_tck.tractogram, new_tck_orig.tractogram)
```

### Step 3: Assign tck = TckFile(...)

```python
tck = TckFile(tractogram)
```

**Verification:**
```python
assert tck_file.read() == open(DATA['empty_tck_fname'], 'rb').read()
```

### Step 4: Call tck.save()

```python
tck.save(tck_file)
```

### Step 5: Call tck_file.seek()

```python
tck_file.seek(0, os.SEEK_SET)
```

### Step 6: Assign new_tck = TckFile.load(...)

```python
new_tck = TckFile.load(tck_file)
```

### Step 7: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_tck.tractogram, tractogram)
```

### Step 8: Assign new_tck_orig = TckFile.load(...)

```python
new_tck_orig = TckFile.load(DATA['empty_tck_fname'])
```

### Step 9: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_tck.tractogram, new_tck_orig.tractogram)
```

### Step 10: Call tck_file.seek()

```python
tck_file.seek(0, os.SEEK_SET)
```

**Verification:**
```python
assert tck_file.read() == open(DATA['empty_tck_fname'], 'rb').read()
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(affine_to_rasmm=np.eye(4))
tck_file = BytesIO()
tck = TckFile(tractogram)
tck.save(tck_file)
tck_file.seek(0, os.SEEK_SET)
new_tck = TckFile.load(tck_file)
assert_tractogram_equal(new_tck.tractogram, tractogram)
new_tck_orig = TckFile.load(DATA['empty_tck_fname'])
assert_tractogram_equal(new_tck.tractogram, new_tck_orig.tractogram)
tck_file.seek(0, os.SEEK_SET)
assert tck_file.read() == open(DATA['empty_tck_fname'], 'rb').read()
```

## Next Steps


---

*Source: test_tck.py:166 | Complexity: Advanced | Last updated: 2026-05-18*