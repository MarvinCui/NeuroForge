# How To: Qvalues

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test qvalues

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sq2 = value

```python
sq2 = np.sqrt(2) / 2.0
```

### Step 2: Assign bvals = value

```python
bvals = 1500 * np.ones(7)
```

### Step 3: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 4: Assign bvecs = np.array(...)

```python
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
```

### Step 5: Assign qvals = value

```python
qvals = np.sqrt(bvals / 6) / (2 * np.pi)
```

### Step 6: Assign bt = gradient_table(...)

```python
bt = gradient_table(bvals, bvecs=bvecs, big_delta=8, small_delta=6)
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(bt.qvals, qvals)
```


## Complete Example

```python
# Workflow
sq2 = np.sqrt(2) / 2.0
bvals = 1500 * np.ones(7)
bvals[0] = 0
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
qvals = np.sqrt(bvals / 6) / (2 * np.pi)
bt = gradient_table(bvals, bvecs=bvecs, big_delta=8, small_delta=6)
npt.assert_almost_equal(bt.qvals, qvals)
```

## Next Steps


---

*Source: test_gradients.py:398 | Complexity: Intermediate | Last updated: 2026-05-18*