# How To: Switch Voxel Sizes From Rasmm

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test switch voxel sizes from rasmm

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

### Step 1: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM)
```

### Step 2: Assign sft_switch = StatefulTractogram(...)

```python
sft_switch = StatefulTractogram(sft.streamlines, FILEPATH_DIX['gs_volume_3mm.nii'], Space.RASMM)
```

### Step 3: Assign tmp_points_rasmm = np.loadtxt(...)

```python
tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
```

### Step 4: Assign tmp_points_voxmm = np.loadtxt(...)

```python
tmp_points_voxmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_voxmm_space.txt'])
```

### Step 5: Call sft_switch.to_rasmm()

```python
sft_switch.to_rasmm()
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(tmp_points_rasmm, sft_switch.streamlines.get_data(), atol=0.001, rtol=1e-06)
```

### Step 7: Call sft_switch.to_voxmm()

```python
sft_switch.to_voxmm()
```

### Step 8: Call npt.assert_allclose()

```python
npt.assert_allclose(tmp_points_voxmm, sft_switch.streamlines.get_data(), atol=0.001, rtol=1e-06)
```


## Complete Example

```python
# Workflow
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.RASMM)
sft_switch = StatefulTractogram(sft.streamlines, FILEPATH_DIX['gs_volume_3mm.nii'], Space.RASMM)
tmp_points_rasmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_rasmm_space.txt'])
tmp_points_voxmm = np.loadtxt(FILEPATH_DIX['gs_streamlines_voxmm_space.txt'])
sft_switch.to_rasmm()
npt.assert_allclose(tmp_points_rasmm, sft_switch.streamlines.get_data(), atol=0.001, rtol=1e-06)
sft_switch.to_voxmm()
npt.assert_allclose(tmp_points_voxmm, sft_switch.streamlines.get_data(), atol=0.001, rtol=1e-06)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:87 | Complexity: Advanced | Last updated: 2026-05-18*