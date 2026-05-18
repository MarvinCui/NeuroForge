# How To: B0S

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test b0s

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
bvals = 1500 * np.ones(8)
```

### Step 3: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 4: Assign unknown = 0

```python
bvals[7] = 0
```

### Step 5: Assign bvecs = np.array(...)

```python
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2], [0, 0, 0]])
```

### Step 6: Assign bt = gradient_table(...)

```python
bt = gradient_table(bvals, bvecs=bvecs)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(np.where(bt.b0s_mask > 0)[0], np.array([0, 7]))
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(np.where(bt.b0s_mask == 0)[0], np.arange(1, 7))
```


## Complete Example

```python
# Workflow
sq2 = np.sqrt(2) / 2.0
bvals = 1500 * np.ones(8)
bvals[0] = 0
bvals[7] = 0
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2], [0, 0, 0]])
bt = gradient_table(bvals, bvecs=bvecs)
npt.assert_array_equal(np.where(bt.b0s_mask > 0)[0], np.array([0, 7]))
npt.assert_array_equal(np.where(bt.b0s_mask == 0)[0], np.arange(1, 7))
```

## Next Steps


---

*Source: test_gradients.py:348 | Complexity: Advanced | Last updated: 2026-05-18*