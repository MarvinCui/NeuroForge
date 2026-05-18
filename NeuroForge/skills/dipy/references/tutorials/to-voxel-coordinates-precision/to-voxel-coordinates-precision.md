# How To: To Voxel Coordinates Precision

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test to voxel coordinates precision

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`


## Step-by-Step Guide

### Step 1: Assign transfo = np.array(...)

```python
transfo = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0]])
```

### Step 2: Assign offset = np.array(...)

```python
offset = np.array([0.5, 0.5, 0.5])
```

### Step 3: Assign failing_strl = value

```python
failing_strl = [np.array([[-0.5000001, 0.0, 0.0], [0.0, 1.0, 0.0]], dtype=np.float32)]
```

### Step 4: Assign indices = _to_voxel_coordinates(...)

```python
indices = _to_voxel_coordinates(failing_strl, transfo, offset)
```

### Step 5: Assign expected_indices = np.array(...)

```python
expected_indices = np.array([[[0, 0, 0], [0, 1, 0]]])
```

### Step 6: Call npt.assert_array_equal()

```python
npt.assert_array_equal(indices, expected_indices)
```


## Complete Example

```python
# Workflow
transfo = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0]])
offset = np.array([0.5, 0.5, 0.5])
failing_strl = [np.array([[-0.5000001, 0.0, 0.0], [0.0, 1.0, 0.0]], dtype=np.float32)]
indices = _to_voxel_coordinates(failing_strl, transfo, offset)
expected_indices = np.array([[[0, 0, 0], [0, 1, 0]]])
npt.assert_array_equal(indices, expected_indices)
```

## Next Steps


---

*Source: test_utils.py:89 | Complexity: Intermediate | Last updated: 2026-05-18*