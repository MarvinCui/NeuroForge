# How To: Transform Centers Of Mass 3D

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: test transform centers of mass 3d

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imaffine`
- `dipy.align.tests.test_parzenhist`
- `dipy.align.transforms`
- `dipy.core`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign trans = np.array(...)

```python
trans = np.array([[1, 0, 0, -t * shape[0]], [0, 1, 0, -t * shape[1]], [0, 0, 1, -t * shape[2]], [0, 0, 0, 1]])
```


## Complete Example

```python
# Workflow
trans = np.array([[1, 0, 0, -t * shape[0]], [0, 1, 0, -t * shape[1]], [0, 0, 1, -t * shape[2]], [0, 0, 0, 1]])
```

## Next Steps


---

*Source: test_imaffine.py:64 | Complexity: Beginner | Last updated: 2026-05-18*