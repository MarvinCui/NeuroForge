# How To: Space Gold Standard

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test space gold standard

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
# Fixtures: ext, space
```

## Step-by-Step Guide

### Step 1: Assign from_space = value

```python
from_space = Space.LPSMM if ext in ['vtk', 'fib'] else Space.RASMM
```

### Step 2: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(FILEPATH_DIX[f'gs_streamlines.{ext}'], FILEPATH_DIX['gs_volume.nii'], to_space=space, from_space=from_space, bbox_valid_check=False)
```

### Step 3: Assign fname = value

```python
fname = FILEPATH_DIX[f'gs_streamlines_{space.value.lower()}_space.txt']
```

### Step 4: Assign tmp_points_vox = np.loadtxt(...)

```python
tmp_points_vox = np.loadtxt(fname)
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(tmp_points_vox, sft.streamlines.get_data(), atol=0.001, rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: ext, space

# Workflow
from_space = Space.LPSMM if ext in ['vtk', 'fib'] else Space.RASMM
sft = load_tractogram(FILEPATH_DIX[f'gs_streamlines.{ext}'], FILEPATH_DIX['gs_volume.nii'], to_space=space, from_space=from_space, bbox_valid_check=False)
fname = FILEPATH_DIX[f'gs_streamlines_{space.value.lower()}_space.txt']
tmp_points_vox = np.loadtxt(fname)
npt.assert_allclose(tmp_points_vox, sft.streamlines.get_data(), atol=0.001, rtol=1e-06)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:69 | Complexity: Intermediate | Last updated: 2026-05-18*