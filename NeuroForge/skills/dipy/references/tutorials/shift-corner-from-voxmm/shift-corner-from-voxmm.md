# How To: Shift Corner From Voxmm

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test shift corner from voxmm

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

### Step 1: Assign sft_1 = load_tractogram(...)

```python
sft_1 = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.VOX)
```

### Step 2: Call sft_1.to_corner()

```python
sft_1.to_corner()
```

### Step 3: Assign bbox_1 = sft_1.compute_bounding_box(...)

```python
bbox_1 = sft_1.compute_bounding_box()
```

### Step 4: Assign sft_2 = load_tractogram(...)

```python
sft_2 = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.VOXMM)
```

### Step 5: Call sft_2.to_corner()

```python
sft_2.to_corner()
```

### Step 6: Call sft_2.to_vox()

```python
sft_2.to_vox()
```

### Step 7: Assign bbox_2 = sft_2.compute_bounding_box(...)

```python
bbox_2 = sft_2.compute_bounding_box()
```

### Step 8: Call npt.assert_allclose()

```python
npt.assert_allclose(bbox_1, bbox_2, atol=0.001, rtol=1e-06)
```


## Complete Example

```python
# Workflow
sft_1 = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.VOX)
sft_1.to_corner()
bbox_1 = sft_1.compute_bounding_box()
sft_2 = load_tractogram(FILEPATH_DIX['gs_streamlines.trk'], FILEPATH_DIX['gs_volume.nii'], to_space=Space.VOXMM)
sft_2.to_corner()
sft_2.to_vox()
bbox_2 = sft_2.compute_bounding_box()
npt.assert_allclose(bbox_1, bbox_2, atol=0.001, rtol=1e-06)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:349 | Complexity: Advanced | Last updated: 2026-05-18*