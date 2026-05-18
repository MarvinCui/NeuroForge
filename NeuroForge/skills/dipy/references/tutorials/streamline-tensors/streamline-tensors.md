# How To: Streamline Tensors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test streamline tensors

## Prerequisites

**Required Modules:**
- `os.path`
- `nibabel`
- `numpy`
- `numpy.testing`
- `scipy.linalg`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.tracking.life`


## Step-by-Step Guide

### Step 1: Assign streamline = value

```python
streamline = [[1, 2, 3], [4, 5, 3], [5, 6, 3]]
```

### Step 2: Assign evals = value

```python
evals = [0.0012, 0.0006, 0.0004]
```

### Step 3: Assign streamline_tensors = life.streamline_tensors(...)

```python
streamline_tensors = life.streamline_tensors(streamline, evals=evals)
```

### Step 4: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(streamline_tensors[0], np.array([[0.0009, 0.0003, 0.0], [0.0003, 0.0009, 0.0], [0.0, 0.0, 0.0004]]))
```

### Step 5: Assign unknown = la.eig(...)

```python
eigvals, eigvecs = la.eig(streamline_tensors[0])
```

### Step 6: Assign eigvecs = value

```python
eigvecs = eigvecs[np.argsort(eigvals)[::-1]]
```

### Step 7: Assign eigvals = value

```python
eigvals = eigvals[np.argsort(eigvals)[::-1]]
```

### Step 8: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(eigvals, np.array([0.0012, 0.0006, 0.0004]))
```

### Step 9: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(eigvecs[0], np.array([0.70710678, -0.70710678, 0.0]))
```

### Step 10: Assign streamline = value

```python
streamline = [[1, 0, 0], [2, 0, 0], [3, 0, 0]]
```

### Step 11: Assign streamline_tensors = life.streamline_tensors(...)

```python
streamline_tensors = life.streamline_tensors(streamline, evals=evals)
```

### Step 12: Assign unknown = la.eig(...)

```python
eigvals, eigvecs = la.eig(t)
```

### Step 13: Assign eigvecs = value

```python
eigvecs = eigvecs[np.argsort(eigvals)[::-1]]
```

### Step 14: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[0], [1, 0, 0]))), 0)
```

### Step 15: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[1], [0, 1, 0]))), 0)
```

### Step 16: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[2], [0, 0, 1]))), 0)
```


## Complete Example

```python
# Workflow
streamline = [[1, 2, 3], [4, 5, 3], [5, 6, 3]]
evals = [0.0012, 0.0006, 0.0004]
streamline_tensors = life.streamline_tensors(streamline, evals=evals)
npt.assert_array_almost_equal(streamline_tensors[0], np.array([[0.0009, 0.0003, 0.0], [0.0003, 0.0009, 0.0], [0.0, 0.0, 0.0004]]))
eigvals, eigvecs = la.eig(streamline_tensors[0])
eigvecs = eigvecs[np.argsort(eigvals)[::-1]]
eigvals = eigvals[np.argsort(eigvals)[::-1]]
npt.assert_array_almost_equal(eigvals, np.array([0.0012, 0.0006, 0.0004]))
npt.assert_array_almost_equal(eigvecs[0], np.array([0.70710678, -0.70710678, 0.0]))
streamline = [[1, 0, 0], [2, 0, 0], [3, 0, 0]]
streamline_tensors = life.streamline_tensors(streamline, evals=evals)
for t in streamline_tensors:
    eigvals, eigvecs = la.eig(t)
    eigvecs = eigvecs[np.argsort(eigvals)[::-1]]
    npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[0], [1, 0, 0]))), 0)
    npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[1], [0, 1, 0]))), 0)
    npt.assert_almost_equal(np.rad2deg(np.arccos(np.dot(eigvecs[2], [0, 0, 1]))), 0)
```

## Next Steps


---

*Source: test_life.py:25 | Complexity: Advanced | Last updated: 2026-05-18*