# How To: From Sfs Dtype Dict Attributes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test from sfs dtype dict attributes

## Prerequisites

**Required Modules:**
- `itertools`
- `os.path`
- `tempfile`
- `urllib.error`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.stateful_surface`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign sfs = load_surface(...)

```python
sfs = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
```

### Step 2: Assign sfs.data_per_vertex = value

```python
sfs.data_per_vertex = {'color_r': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16), 'color_g': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16), 'color_b': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16)}
```

### Step 3: Assign dtype_dict = value

```python
dtype_dict = {'vertices': np.float16, 'faces': np.int32, 'dpp': {'color_r': np.uint8, 'color_g': np.uint8, 'color_b': np.uint8}}
```

### Step 4: Assign sfs.dtype_dict = dtype_dict

```python
sfs.dtype_dict = dtype_dict
```

### Step 5: Assign new_sfs = StatefulSurface.from_sfs(...)

```python
new_sfs = StatefulSurface.from_sfs(sfs.vertices, sfs, data_per_vertex=sfs.data_per_vertex)
```

### Step 6: Call recursive_compare()

```python
recursive_compare(new_sfs.dtype_dict, dtype_dict)
```

### Step 7: Call recursive_compare()

```python
recursive_compare(sfs.dtype_dict, dtype_dict)
```

### Step 8: Call npt.assert_()

```python
npt.assert_(False, msg='from_sfs() should not modify the dtype_dict.')
```


## Complete Example

```python
# Workflow
sfs = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
sfs.data_per_vertex = {'color_r': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16), 'color_g': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16), 'color_b': np.zeros((sfs.vertices.shape[0], 3), dtype=np.uint16)}
dtype_dict = {'vertices': np.float16, 'faces': np.int32, 'dpp': {'color_r': np.uint8, 'color_g': np.uint8, 'color_b': np.uint8}}
sfs.dtype_dict = dtype_dict
new_sfs = StatefulSurface.from_sfs(sfs.vertices, sfs, data_per_vertex=sfs.data_per_vertex)
try:
    recursive_compare(new_sfs.dtype_dict, dtype_dict)
    recursive_compare(sfs.dtype_dict, dtype_dict)
except ValueError:
    npt.assert_(False, msg='from_sfs() should not modify the dtype_dict.')
```

## Next Steps


---

*Source: test_stateful_surface.py:399 | Complexity: Advanced | Last updated: 2026-05-18*