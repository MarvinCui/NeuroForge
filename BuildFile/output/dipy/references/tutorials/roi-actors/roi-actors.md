# How To: Roi Actors

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Fixture to create a ROI Actors.

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.viz.horizon.tab.base`
- `dipy.viz.horizon.tab.roi`
- `fury.actor`


## Step-by-Step Guide

### Step 1: 'Fixture to create a ROI Actors.'

```python
'Fixture to create a ROI Actors.'
```

### Step 2: Assign affine = np.array(...)

```python
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 3: Assign img = np.zeros(...)

```python
img = np.zeros((197, 233, 189))
```

### Step 4: Assign unknown = 1

```python
img[0:25, :, :] = 1
```

### Step 5: Assign roi_actor = contour_from_roi(...)

```python
roi_actor = contour_from_roi(img, affine=affine)
```


## Complete Example

```python
# Workflow
'Fixture to create a ROI Actors.'
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
img = np.zeros((197, 233, 189))
img[0:25, :, :] = 1
roi_actor = contour_from_roi(img, affine=affine)
return [roi_actor]
```

## Next Steps


---

*Source: test_roi.py:21 | Complexity: Intermediate | Last updated: 2026-05-18*