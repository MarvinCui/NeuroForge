# How To: Random Point Gray

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random point gray

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
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.tck'], FILEPATH_DIX['gs_volume.nii'])
```

### Step 2: Assign random_colors = rng.integers(...)

```python
random_colors = rng.integers(0, 255, (13, 8, 1))
```

### Step 3: Assign coloring_dict = value

```python
coloring_dict = {'color_x': random_colors, 'color_y': random_colors, 'color_z': random_colors}
```

### Step 4: Assign sft.data_per_point = coloring_dict

```python
sft.data_per_point = coloring_dict
```

### Step 5: Call npt.assert_()

```python
npt.assert_(True)
```

### Step 6: Call save_tractogram()

```python
save_tractogram(sft, Path(tmp_dir) / 'random_points_gray.trk')
```

### Step 7: Call npt.assert_()

```python
npt.assert_(False)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.tck'], FILEPATH_DIX['gs_volume.nii'])
random_colors = rng.integers(0, 255, (13, 8, 1))
coloring_dict = {'color_x': random_colors, 'color_y': random_colors, 'color_z': random_colors}
try:
    sft.data_per_point = coloring_dict
    with TemporaryDirectory() as tmp_dir:
        save_tractogram(sft, Path(tmp_dir) / 'random_points_gray.trk')
    npt.assert_(True)
except ValueError:
    npt.assert_(False)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:478 | Complexity: Advanced | Last updated: 2026-05-18*