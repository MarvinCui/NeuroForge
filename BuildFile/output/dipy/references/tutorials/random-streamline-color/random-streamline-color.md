# How To: Random Streamline Color

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random streamline color

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

### Step 2: Assign uniform_colors_x = rng.integers(...)

```python
uniform_colors_x = rng.integers(0, 255, (13, 1))
```

### Step 3: Assign uniform_colors_y = rng.integers(...)

```python
uniform_colors_y = rng.integers(0, 255, (13, 1))
```

### Step 4: Assign uniform_colors_z = rng.integers(...)

```python
uniform_colors_z = rng.integers(0, 255, (13, 1))
```

### Step 5: Assign uniform_colors_x = np.expand_dims(...)

```python
uniform_colors_x = np.expand_dims(np.repeat(uniform_colors_x, 8, axis=1), axis=-1)
```

### Step 6: Assign uniform_colors_y = np.expand_dims(...)

```python
uniform_colors_y = np.expand_dims(np.repeat(uniform_colors_y, 8, axis=1), axis=-1)
```

### Step 7: Assign uniform_colors_z = np.expand_dims(...)

```python
uniform_colors_z = np.expand_dims(np.repeat(uniform_colors_z, 8, axis=1), axis=-1)
```

### Step 8: Assign coloring_dict = value

```python
coloring_dict = {'color_x': uniform_colors_x, 'color_y': uniform_colors_y, 'color_z': uniform_colors_z}
```

### Step 9: Assign sft.data_per_point = coloring_dict

```python
sft.data_per_point = coloring_dict
```

### Step 10: Call npt.assert_()

```python
npt.assert_(True)
```

### Step 11: Call save_tractogram()

```python
save_tractogram(sft, Path(tmp_dir) / 'random_streamlines_color.trk')
```

### Step 12: Call npt.assert_()

```python
npt.assert_(False)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
sft = load_tractogram(FILEPATH_DIX['gs_streamlines.tck'], FILEPATH_DIX['gs_volume.nii'])
uniform_colors_x = rng.integers(0, 255, (13, 1))
uniform_colors_y = rng.integers(0, 255, (13, 1))
uniform_colors_z = rng.integers(0, 255, (13, 1))
uniform_colors_x = np.expand_dims(np.repeat(uniform_colors_x, 8, axis=1), axis=-1)
uniform_colors_y = np.expand_dims(np.repeat(uniform_colors_y, 8, axis=1), axis=-1)
uniform_colors_z = np.expand_dims(np.repeat(uniform_colors_z, 8, axis=1), axis=-1)
coloring_dict = {'color_x': uniform_colors_x, 'color_y': uniform_colors_y, 'color_z': uniform_colors_z}
try:
    sft.data_per_point = coloring_dict
    with TemporaryDirectory() as tmp_dir:
        save_tractogram(sft, Path(tmp_dir) / 'random_streamlines_color.trk')
    npt.assert_(True)
except (TypeError, ValueError):
    npt.assert_(False)
```

## Next Steps


---

*Source: test_stateful_tractogram.py:500 | Complexity: Advanced | Last updated: 2026-05-18*