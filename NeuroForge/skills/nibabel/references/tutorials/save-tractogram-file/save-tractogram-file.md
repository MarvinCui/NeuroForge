# How To: Save Tractogram File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test save tractogram file

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
assert_tractogram_equal(tfile.tractogram, tractogram)
```

### Step 2: Assign trk_file = trk.TrkFile(...)

```python
trk_file = trk.TrkFile(tractogram)
```

**Verification:**
```python
assert_tractogram_equal(tfile.tractogram, tractogram)
```

### Step 3: Call nib.streamlines.save()

```python
nib.streamlines.save(trk_file, 'dummy.trk', header={})
```

### Step 4: Assign trk_file = trk.TrkFile(...)

```python
trk_file = trk.TrkFile(tractogram)
```

### Step 5: Call nib.streamlines.save()

```python
nib.streamlines.save(trk_file, 'dummy.trk')
```

### Step 6: Assign tfile = nib.streamlines.load(...)

```python
tfile = nib.streamlines.load('dummy.trk', lazy_load=False)
```

### Step 7: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tfile.tractogram, tractogram)
```

### Step 8: Call nib.streamlines.save()

```python
nib.streamlines.save(trk_file, Path('dummy.trk'))
```

### Step 9: Assign tfile = nib.streamlines.load(...)

```python
tfile = nib.streamlines.load('dummy.trk', lazy_load=False)
```

### Step 10: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tfile.tractogram, tractogram)
```

### Step 11: Call nib.streamlines.save()

```python
nib.streamlines.save(trk_file, 'dummy.tck', header={})
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(DATA['streamlines'], affine_to_rasmm=np.eye(4))
trk_file = trk.TrkFile(tractogram)
with pytest.raises(ValueError):
    nib.streamlines.save(trk_file, 'dummy.trk', header={})
with pytest.warns(ExtensionWarning, match='extension'):
    trk_file = trk.TrkFile(tractogram)
    with pytest.raises(ValueError):
        nib.streamlines.save(trk_file, 'dummy.tck', header={})
with InTemporaryDirectory():
    nib.streamlines.save(trk_file, 'dummy.trk')
    tfile = nib.streamlines.load('dummy.trk', lazy_load=False)
    assert_tractogram_equal(tfile.tractogram, tractogram)
with InTemporaryDirectory():
    nib.streamlines.save(trk_file, Path('dummy.trk'))
    tfile = nib.streamlines.load('dummy.trk', lazy_load=False)
    assert_tractogram_equal(tfile.tractogram, tractogram)
```

## Next Steps


---

*Source: test_streamlines.py:212 | Complexity: Advanced | Last updated: 2026-05-18*