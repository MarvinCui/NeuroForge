# How To: Direct Trx Loading

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test direct trx loading

## Prerequisites

**Required Modules:**
- `copy`
- `itertools`
- `pathlib`
- `sys`
- `tempfile`
- `urllib.error`
- `numpy`
- `numpy.testing`
- `pytest`
- `trx.trx_file_memmap`
- `dipy.data`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.io.utils`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign trx = tmm.load(...)

```python
trx = tmm.load(FILEPATH_DIX['gs_streamlines.trx'])
```

**Verification:**
```python
assert Path(tmp_dir).is_dir()
```

### Step 2: Assign tmp_dir = deepcopy(...)

```python
tmp_dir = deepcopy(trx._uncompressed_folder_handle.name)
```

**Verification:**
```python
assert not Path(tmp_dir).is_dir()
```

### Step 3: Assign sft = trx.to_sft(...)

```python
sft = trx.to_sft()
```

### Step 4: Assign tmp_points_vox = np.loadtxt(...)

```python
tmp_points_vox = np.loadtxt(FILEPATH_DIX['gs_streamlines_vox_space.txt'])
```

### Step 5: Assign tmp_points_rasmm = np.loadtxt(...)

```python
tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
```

### Step 6: Call trx.close()

```python
trx.close()
```

**Verification:**
```python
assert not Path(tmp_dir).is_dir()
```

### Step 7: Call npt.assert_allclose()

```python
npt.assert_allclose(sft.streamlines._data, tmp_points_rasmm, rtol=0.0001, atol=1e-06)
```

### Step 8: Call sft.to_vox()

```python
sft.to_vox()
```

### Step 9: Call npt.assert_allclose()

```python
npt.assert_allclose(sft.streamlines._data, tmp_points_vox, rtol=0.0001, atol=1e-06)
```


## Complete Example

```python
# Workflow
trx = tmm.load(FILEPATH_DIX['gs_streamlines.trx'])
tmp_dir = deepcopy(trx._uncompressed_folder_handle.name)
assert Path(tmp_dir).is_dir()
sft = trx.to_sft()
tmp_points_vox = np.loadtxt(FILEPATH_DIX['gs_streamlines_vox_space.txt'])
tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
trx.close()
assert not Path(tmp_dir).is_dir()
npt.assert_allclose(sft.streamlines._data, tmp_points_rasmm, rtol=0.0001, atol=1e-06)
sft.to_vox()
npt.assert_allclose(sft.streamlines._data, tmp_points_vox, rtol=0.0001, atol=1e-06)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:50 | Complexity: Advanced | Last updated: 2026-05-18*