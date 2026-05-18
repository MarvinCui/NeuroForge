# How To: Set Dtype Dict Attributes

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test set dtype dict attributes

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
sfs.data_per_vertex = {'normal': np.zeros((sfs.vertices.shape[0], 3), dtype=np.float16)}
```

### Step 3: Assign dtype_dict = value

```python
dtype_dict = {'vertices': np.float16, 'faces': np.int32, 'dpp': {'normal': np.float16}}
```

### Step 4: Assign sfs.dtype_dict = dtype_dict

```python
sfs.dtype_dict = dtype_dict
```

### Step 5: Call recursive_compare()

```python
recursive_compare(dtype_dict, sfs.dtype_dict)
```

### Step 6: Call npt.assert_()

```python
npt.assert_(False, msg='dtype_dict should be identical after set.')
```


## Complete Example

```python
# Workflow
sfs = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
sfs.data_per_vertex = {'normal': np.zeros((sfs.vertices.shape[0], 3), dtype=np.float16)}
dtype_dict = {'vertices': np.float16, 'faces': np.int32, 'dpp': {'normal': np.float16}}
sfs.dtype_dict = dtype_dict
try:
    recursive_compare(dtype_dict, sfs.dtype_dict)
except ValueError:
    npt.assert_(False, msg='dtype_dict should be identical after set.')
```

## Next Steps


---

*Source: test_stateful_surface.py:329 | Complexity: Advanced | Last updated: 2026-05-18*