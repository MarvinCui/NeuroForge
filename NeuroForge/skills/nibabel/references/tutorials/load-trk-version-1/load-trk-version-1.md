# How To: Load Trk Version 1

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load trk version 1

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

### Step 1: Assign unknown = self.trk_with_bytes(...)

```python
trk_struct, trk_bytes = self.trk_with_bytes()
```

**Verification:**
```python
assert_array_equal(trk.affine, np.diag([2, 3, 4, 1]))
```

### Step 2: Assign unknown = np.diag(...)

```python
trk_struct[Field.VOXEL_TO_RASMM] = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_array_equal(trk.affine, np.eye(4))
```

### Step 3: Assign trk = TrkFile.load(...)

```python
trk = TrkFile.load(BytesIO(trk_bytes))
```

**Verification:**
```python
assert_array_equal(trk.header['version'], 1)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(trk.affine, np.diag([2, 3, 4, 1]))
```

### Step 5: Assign unknown = 1

```python
trk_struct['version'] = 1
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(trk.affine, np.eye(4))
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(trk.header['version'], 1)
```

### Step 8: Assign trk = TrkFile.load(...)

```python
trk = TrkFile.load(BytesIO(trk_bytes))
```


## Complete Example

```python
# Workflow
trk_struct, trk_bytes = self.trk_with_bytes()
trk_struct[Field.VOXEL_TO_RASMM] = np.diag([2, 3, 4, 1])
trk = TrkFile.load(BytesIO(trk_bytes))
assert_array_equal(trk.affine, np.diag([2, 3, 4, 1]))
trk_struct['version'] = 1
with pytest.warns(HeaderWarning, match='identity'):
    trk = TrkFile.load(BytesIO(trk_bytes))
assert_array_equal(trk.affine, np.eye(4))
assert_array_equal(trk.header['version'], 1)
```

## Next Steps


---

*Source: test_trk.py:186 | Complexity: Advanced | Last updated: 2026-05-18*