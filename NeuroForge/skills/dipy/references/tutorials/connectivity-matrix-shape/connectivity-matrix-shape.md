# How To: Connectivity Matrix Shape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test connectivity matrix shape

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

### Step 1: Assign labels = np.zeros(...)

```python
labels = np.zeros((3, 3, 3), dtype=int)
```

### Step 2: Assign unknown = 1

```python
labels[:, :, 1] = 1
```

### Step 3: Assign unknown = 2

```python
labels[:, :, 2] = 2
```

### Step 4: Assign streamlines = value

```python
streamlines = [np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.5], [0.0, 0.0, 1.0]]), np.array([[0.0, 1.0, 1.0], [0.0, 1.0, 0.5], [0.0, 1.0, 0.0]])]
```

### Step 5: Assign matrix = connectivity_matrix(...)

```python
matrix = connectivity_matrix(streamlines, np.eye(4), labels)
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(matrix.shape, (3, 3))
```


## Complete Example

```python
# Workflow
labels = np.zeros((3, 3, 3), dtype=int)
labels[:, :, 1] = 1
labels[:, :, 2] = 2
streamlines = [np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 0.5], [0.0, 0.0, 1.0]]), np.array([[0.0, 1.0, 1.0], [0.0, 1.0, 0.5], [0.0, 1.0, 0.0]])]
matrix = connectivity_matrix(streamlines, np.eye(4), labels)
npt.assert_equal(matrix.shape, (3, 3))
```

## Next Steps


---

*Source: test_utils.py:745 | Complexity: Intermediate | Last updated: 2026-05-18*