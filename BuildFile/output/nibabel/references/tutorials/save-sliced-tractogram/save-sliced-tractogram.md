# How To: Save Sliced Tractogram

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test save sliced tractogram

## Prerequisites

**Required Modules:**
- `os`
- `unittest`
- `warnings`
- `io`
- `os.path`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.testing`
- `nibabel.tmpdirs`
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
assert_tractogram_equal(tfile.tractogram, tractogram[::2])
```

### Step 2: Assign original_tractogram = tractogram.copy(...)

```python
original_tractogram = tractogram.copy()
```

**Verification:**
```python
assert_tractogram_equal(tractogram, original_tractogram)
```

### Step 3: Assign filename = value

```python
filename = 'streamlines' + ext
```

### Step 4: Call nib.streamlines.save()

```python
nib.streamlines.save(tractogram[::2], filename)
```

### Step 5: Assign tfile = nib.streamlines.load(...)

```python
tfile = nib.streamlines.load(filename, lazy_load=False)
```

### Step 6: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tfile.tractogram, tractogram[::2])
```

### Step 7: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tractogram, original_tractogram)
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(DATA['streamlines'], affine_to_rasmm=np.eye(4))
original_tractogram = tractogram.copy()
for ext in FORMATS:
    with InTemporaryDirectory():
        filename = 'streamlines' + ext
        nib.streamlines.save(tractogram[::2], filename)
        tfile = nib.streamlines.load(filename, lazy_load=False)
        assert_tractogram_equal(tfile.tractogram, tractogram[::2])
        assert_tractogram_equal(tractogram, original_tractogram)
```

## Next Steps


---

*Source: test_streamlines.py:294 | Complexity: Intermediate | Last updated: 2026-05-18*