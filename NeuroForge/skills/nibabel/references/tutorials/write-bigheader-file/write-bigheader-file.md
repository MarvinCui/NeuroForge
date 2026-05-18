# How To: Write Bigheader File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write bigheader file

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
tractogram = Tractogram(DATA['streamlines'], affine_to_rasmm=np.eye(4))
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
assert new_tck.header['_offset_data'] == 99
```

### Step 3: Assign tck = TckFile(...)

```python
tck = TckFile(tractogram)
```

**Verification:**
```python
assert_tractogram_equal(new_tck.tractogram, tractogram)
```

### Step 4: Assign unknown = value

```python
tck.header['new_entry'] = ' ' * 20
```

**Verification:**
```python
assert new_tck.header['_offset_data'] == 101
```

### Step 5: Call tck.save()

```python
tck.save(tck_file)
```

### Step 6: Call tck_file.seek()

```python
tck_file.seek(0, os.SEEK_SET)
```

### Step 7: Assign new_tck = TckFile.load(...)

```python
new_tck = TckFile.load(tck_file)
```

### Step 8: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_tck.tractogram, tractogram)
```

**Verification:**
```python
assert new_tck.header['_offset_data'] == 99
```

### Step 9: Assign tck_file = BytesIO(...)

```python
tck_file = BytesIO()
```

### Step 10: Assign tck = TckFile(...)

```python
tck = TckFile(tractogram)
```

### Step 11: Assign unknown = value

```python
tck.header['new_entry'] = ' ' * 21
```

### Step 12: Call tck.save()

```python
tck.save(tck_file)
```

### Step 13: Call tck_file.seek()

```python
tck_file.seek(0, os.SEEK_SET)
```

### Step 14: Assign new_tck = TckFile.load(...)

```python
new_tck = TckFile.load(tck_file)
```

### Step 15: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_tck.tractogram, tractogram)
```

**Verification:**
```python
assert new_tck.header['_offset_data'] == 101
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(DATA['streamlines'], affine_to_rasmm=np.eye(4))
tck_file = BytesIO()
tck = TckFile(tractogram)
tck.header['new_entry'] = ' ' * 20
tck.save(tck_file)
tck_file.seek(0, os.SEEK_SET)
new_tck = TckFile.load(tck_file)
assert_tractogram_equal(new_tck.tractogram, tractogram)
assert new_tck.header['_offset_data'] == 99
tck_file = BytesIO()
tck = TckFile(tractogram)
tck.header['new_entry'] = ' ' * 21
tck.save(tck_file)
tck_file.seek(0, os.SEEK_SET)
new_tck = TckFile.load(tck_file)
assert_tractogram_equal(new_tck.tractogram, tractogram)
assert new_tck.header['_offset_data'] == 101
```

## Next Steps


---

*Source: test_tck.py:207 | Complexity: Advanced | Last updated: 2026-05-18*