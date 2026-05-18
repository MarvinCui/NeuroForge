# How To: Write Too Many Scalars And Properties

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write too many scalars and properties

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

### Step 1: Assign data_per_point = value

```python
data_per_point = {}
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 2: Assign unknown = value

```python
data_per_point[f'#{i + 1}'] = DATA['fa']
```

**Verification:**
```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 3: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_point=data_per_point, affine_to_rasmm=np.eye(4))
```

### Step 4: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 5: Assign data_per_streamline = value

```python
data_per_streamline = {}
```

### Step 6: Assign unknown = value

```python
data_per_streamline[f'#{i + 1}'] = DATA['mean_torsion']
```

### Step 7: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline)
```

### Step 8: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 9: Assign unknown = value

```python
data_per_point[f'#{i}'] = DATA['fa']
```

### Step 10: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_point=data_per_point, affine_to_rasmm=np.eye(4))
```

### Step 11: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 12: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 13: Call trk.save()

```python
trk.save(trk_file)
```

### Step 14: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 15: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file, lazy_load=False)
```

### Step 16: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 17: Call trk.save()

```python
trk.save(BytesIO())
```

### Step 18: Assign unknown = value

```python
data_per_streamline[f'#{i}'] = DATA['mean_torsion']
```

### Step 19: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
```

### Step 20: Assign trk_file = BytesIO(...)

```python
trk_file = BytesIO()
```

### Step 21: Assign trk = TrkFile(...)

```python
trk = TrkFile(tractogram)
```

### Step 22: Call trk.save()

```python
trk.save(trk_file)
```

### Step 23: Call trk_file.seek()

```python
trk_file.seek(0, os.SEEK_SET)
```

### Step 24: Assign new_trk = TrkFile.load(...)

```python
new_trk = TrkFile.load(trk_file, lazy_load=False)
```

### Step 25: Call assert_tractogram_equal()

```python
assert_tractogram_equal(new_trk.tractogram, tractogram)
```

### Step 26: Call trk.save()

```python
trk.save(BytesIO())
```


## Complete Example

```python
# Workflow
data_per_point = {}
for i in range(10):
    data_per_point[f'#{i}'] = DATA['fa']
    tractogram = Tractogram(DATA['streamlines'], data_per_point=data_per_point, affine_to_rasmm=np.eye(4))
    trk_file = BytesIO()
    trk = TrkFile(tractogram)
    trk.save(trk_file)
    trk_file.seek(0, os.SEEK_SET)
    new_trk = TrkFile.load(trk_file, lazy_load=False)
    assert_tractogram_equal(new_trk.tractogram, tractogram)
data_per_point[f'#{i + 1}'] = DATA['fa']
tractogram = Tractogram(DATA['streamlines'], data_per_point=data_per_point, affine_to_rasmm=np.eye(4))
trk = TrkFile(tractogram)
with pytest.raises(ValueError):
    trk.save(BytesIO())
data_per_streamline = {}
for i in range(10):
    data_per_streamline[f'#{i}'] = DATA['mean_torsion']
    tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline, affine_to_rasmm=np.eye(4))
    trk_file = BytesIO()
    trk = TrkFile(tractogram)
    trk.save(trk_file)
    trk_file.seek(0, os.SEEK_SET)
    new_trk = TrkFile.load(trk_file, lazy_load=False)
    assert_tractogram_equal(new_trk.tractogram, tractogram)
data_per_streamline[f'#{i + 1}'] = DATA['mean_torsion']
tractogram = Tractogram(DATA['streamlines'], data_per_streamline=data_per_streamline)
trk = TrkFile(tractogram)
with pytest.raises(ValueError):
    trk.save(BytesIO())
```

## Next Steps


---

*Source: test_trk.py:377 | Complexity: Advanced | Last updated: 2026-05-18*