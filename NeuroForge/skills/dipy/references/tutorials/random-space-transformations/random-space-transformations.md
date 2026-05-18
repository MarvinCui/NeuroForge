# How To: Random Space Transformations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random space transformations

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
sfs = load_surface(FILEPATH_DIX['naf_lh.pial'], FILEPATH_DIX['naf_mni_masked.nii.gz'])
```

### Step 2: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 3: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 4: Assign initial_vertices = sfs.vertices.copy(...)

```python
initial_vertices = sfs.vertices.copy()
```

### Step 5: Call sfs.to_rasmm()

```python
sfs.to_rasmm()
```

### Step 6: Call sfs.to_center()

```python
sfs.to_center()
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(initial_vertices, sfs.vertices, decimal=5)
```

### Step 8: Assign space = np.random.choice(...)

```python
space = np.random.choice(SPACES, 1, replace=False)
```

### Step 9: Assign origin = np.random.choice(...)

```python
origin = np.random.choice(ORIGINS, 1, replace=False)
```

### Step 10: Call sfs.to_space()

```python
sfs.to_space(space)
```

### Step 11: Call sfs.to_origin()

```python
sfs.to_origin(origin)
```


## Complete Example

```python
# Workflow
sfs = load_surface(FILEPATH_DIX['naf_lh.pial'], FILEPATH_DIX['naf_mni_masked.nii.gz'])
sfs.to_rasmm()
sfs.to_center()
initial_vertices = sfs.vertices.copy()
for _ in range(100):
    space = np.random.choice(SPACES, 1, replace=False)
    origin = np.random.choice(ORIGINS, 1, replace=False)
    sfs.to_space(space)
    sfs.to_origin(origin)
sfs.to_rasmm()
sfs.to_center()
npt.assert_almost_equal(initial_vertices, sfs.vertices, decimal=5)
```

## Next Steps


---

*Source: test_stateful_surface.py:220 | Complexity: Advanced | Last updated: 2026-05-18*