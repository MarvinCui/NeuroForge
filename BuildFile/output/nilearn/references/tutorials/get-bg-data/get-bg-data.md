# How To: Get Bg Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface._utils.get_bg_data for valid inputs.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.plotting.surface._utils`
- `nilearn.surface`
- `nilearn.surface.utils`


## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface._utils.get_bg_data for valid inputs.'

```python
'Test nilearn.plotting.surface._utils.get_bg_data for valid inputs.'
```

**Verification:**
```python
assert np.allclose(bg_data, np.array([0.5, 0.5, 0.5, 0.5, 0.5]))
```

### Step 2: Assign bg_data = get_bg_data(...)

```python
bg_data = get_bg_data(None, 5)
```

**Verification:**
```python
assert np.allclose(bg_data, load_surf_data(bg_map))
```

### Step 3: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

### Step 4: Assign bg_map = np.sign(...)

```python
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
```

### Step 5: Assign bg_data = get_bg_data(...)

```python
bg_data = get_bg_data(bg_map, len(bg_map))
```

**Verification:**
```python
assert np.allclose(bg_data, load_surf_data(bg_map))
```


## Complete Example

```python
# Workflow
'Test nilearn.plotting.surface._utils.get_bg_data for valid inputs.'
bg_data = get_bg_data(None, 5)
assert np.allclose(bg_data, np.array([0.5, 0.5, 0.5, 0.5, 0.5]))
fsaverage = fetch_surf_fsaverage()
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
bg_data = get_bg_data(bg_map, len(bg_map))
assert np.allclose(bg_data, load_surf_data(bg_map))
```

## Next Steps


---

*Source: test_utils.py:211 | Complexity: Intermediate | Last updated: 2026-05-18*