# How To: Write Optional Header Fields

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write optional header fields

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
tractogram = Tractogram(affine_to_rasmm=np.eye(4))
```

**Verification:**
```python
assert 'extra' not in new_trk.header
```

### Step 2: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 3: Assign header = value

```python
header = {'extra': 1234}
```

### Step 4: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram, header)
```

### Step 5: Call trk.save()

```python
trk.save(trk_file)
```

### Step 6: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 7: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file)
```

**Verification:**
```python
assert 'extra' not in new_trk.header
```


## Complete Example

```python
# Workflow
tractogram = Tractogram(affine_to_rasmm=np.eye(4))
trk_file = BytesIO()
header = {'extra': 1234}
trk = TrkFile(tractogram, header)
trk.save(trk_file)
trk_file.seek(0, os.SEEK_SET)
new_trk = TrkFile.load(trk_file)
assert 'extra' not in new_trk.header
```

## Next Steps


---

*Source: test_trk.py:363 | Complexity: Intermediate | Last updated: 2026-05-18*