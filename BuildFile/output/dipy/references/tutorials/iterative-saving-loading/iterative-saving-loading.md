# How To: Iterative Saving Loading

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test iterative saving loading

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: ext
```

## Step-by-Step Guide

### Step 1: Assign from_space = value

```python
from_space = Space.LPSMM if ext in ['vtk', 'fib'] else Space.RASMM
```

### Step 2: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(FILEPATH_DIX[f'gs_streamlines.{ext}'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM, from_space=from_space)
```

### Step 3: Call save_tractogram()

```python
save_tractogram(sft, Path(tmp_dir) / f'gs_iter.{ext}')
```

### Step 4: Assign tmp_points_rasmm = np.loadtxt(...)

```python
tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
```

### Step 5: Assign sft_iter = load_tractogram(...)

```python
sft_iter = load_tractogram(Path(tmp_dir) / f'gs_iter.{ext}', FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM)
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(tmp_points_rasmm, sft_iter.streamlines.get_data(), atol=0.001, rtol=1e-06)
```

### Step 7: Call save_tractogram()

```python
save_tractogram(sft_iter, Path(tmp_dir) / f'gs_iter.{ext}')
```


## Complete Example

```python
# Setup
# Fixtures: ext

# Workflow
from_space = Space.LPSMM if ext in ['vtk', 'fib'] else Space.RASMM
sft = load_tractogram(FILEPATH_DIX[f'gs_streamlines.{ext}'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM, from_space=from_space)
with TemporaryDirectory() as tmp_dir:
    save_tractogram(sft, Path(tmp_dir) / f'gs_iter.{ext}')
    tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
    for _ in range(100):
        sft_iter = load_tractogram(Path(tmp_dir) / f'gs_iter.{ext}', FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM)
        npt.assert_allclose(tmp_points_rasmm, sft_iter.streamlines.get_data(), atol=0.001, rtol=1e-06)
        save_tractogram(sft_iter, Path(tmp_dir) / f'gs_iter.{ext}')
```

## Next Steps


---

*Source: test_stateful_tractogram.py:252 | Complexity: Intermediate | Last updated: 2026-05-18*