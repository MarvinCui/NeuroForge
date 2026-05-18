# How To: Set Partial Dtype Dict Attributes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test set partial dtype dict attributes

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
dtype_dict = {'vertices': np.float16, 'faces': np.int32}
```

### Step 4: Assign dpp_dtype_dict = value

```python
dpp_dtype_dict = {'normal': np.float16}
```

### Step 5: Assign sfs.dtype_dict = dtype_dict

```python
sfs.dtype_dict = dtype_dict
```

### Step 6: Call recursive_compare()

```python
recursive_compare(dtype_dict['vertices'], sfs.dtype_dict['vertices'])
```

### Step 7: Call recursive_compare()

```python
recursive_compare(dtype_dict['faces'], sfs.dtype_dict['faces'])
```

### Step 8: Call recursive_compare()

```python
recursive_compare(dpp_dtype_dict, sfs.dtype_dict['dpp'])
```

### Step 9: Call npt.assert_()

```python
npt.assert_(False, msg='Partial use of dtype_dict should apply only to the relevant portions.')
```


## Complete Example

```python
# Workflow
sfs = load_surface(FILEPATH_DIX['gs_mesh_rasmm_center.ply'], FILEPATH_DIX['gs_volume.nii'])
sfs.data_per_vertex = {'normal': np.zeros((sfs.vertices.shape[0], 3), dtype=np.float16)}
dtype_dict = {'vertices': np.float16, 'faces': np.int32}
dpp_dtype_dict = {'normal': np.float16}
sfs.dtype_dict = dtype_dict
try:
    recursive_compare(dtype_dict['vertices'], sfs.dtype_dict['vertices'])
    recursive_compare(dtype_dict['faces'], sfs.dtype_dict['faces'])
    recursive_compare(dpp_dtype_dict, sfs.dtype_dict['dpp'])
except ValueError:
    npt.assert_(False, msg='Partial use of dtype_dict should apply only to the relevant portions.')
```

## Next Steps


---

*Source: test_stateful_surface.py:350 | Complexity: Advanced | Last updated: 2026-05-18*