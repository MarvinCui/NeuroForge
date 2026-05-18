# How To: Gradient Table From Bvals Bvecs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gradient table from bvals bvecs

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
sq2 = np.sqrt(2) / 2
```

### Step 2: Assign bvals = value

```python
bvals = [0, 1, 2, 3, 4, 5, 6, 0]
```

### Step 3: Assign bvecs = np.array(...)

```python
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2], [0, 0, 0]])
```

### Step 4: Assign gt = gradient_table_from_bvals_bvecs(...)

```python
gt = gradient_table_from_bvals_bvecs(bvals, bvecs, b0_threshold=0)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.bvecs, bvecs)
```

### Step 6: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.bvals, bvals)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.gradients, np.reshape(bvals, (-1, 1)) * bvecs)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.b0s_mask, [1, 0, 0, 0, 0, 0, 0, 1])
```

### Step 9: Assign new_bvecs = bvecs.copy(...)

```python
new_bvecs = bvecs.copy()
```

### Step 10: Assign unknown = value

```python
new_bvecs[[0, -1]] = np.nan
```

### Step 11: Assign gt = gradient_table_from_bvals_bvecs(...)

```python
gt = gradient_table_from_bvals_bvecs(bvals, new_bvecs, b0_threshold=0)
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.bvecs, bvecs)
```

### Step 13: Assign bad_bvals = value

```python
bad_bvals = [2, 1, 2, 3, 4, 5, 6, 0]
```

### Step 14: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
```

### Step 15: Assign bad_bvals = np.ones(...)

```python
bad_bvals = np.ones(7)
```

### Step 16: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
```

### Step 17: Assign bad_bvals = value

```python
bad_bvals = [-1, -1, -1, -5, -6, -10]
```

### Step 18: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
```

### Step 19: Assign bad_bvals = np.ones(...)

```python
bad_bvals = np.ones((1, 8))
```

### Step 20: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
```

### Step 21: Assign bad_bvecs = np.ones(...)

```python
bad_bvecs = np.ones((1, 8, 3))
```

### Step 22: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
```

### Step 23: Assign bad_bvecs = np.ones(...)

```python
bad_bvecs = np.ones((8, 2))
```

### Step 24: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
```

### Step 25: Assign bad_bvecs = value

```python
bad_bvecs = bvecs * 2
```

### Step 26: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
```

### Step 27: Assign gt = gradient_table_from_bvals_bvecs(...)

```python
gt = gradient_table_from_bvals_bvecs(bvals, bvecs, b0_threshold=0, big_delta=5, small_delta=2)
```

### Step 28: Call npt.assert_equal()

```python
npt.assert_equal(gt.big_delta, 5)
```

### Step 29: Call npt.assert_equal()

```python
npt.assert_equal(gt.small_delta, 2)
```


## Complete Example

```python
# Workflow
sq2 = np.sqrt(2) / 2
bvals = [0, 1, 2, 3, 4, 5, 6, 0]
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2], [0, 0, 0]])
gt = gradient_table_from_bvals_bvecs(bvals, bvecs, b0_threshold=0)
npt.assert_array_equal(gt.bvecs, bvecs)
npt.assert_array_equal(gt.bvals, bvals)
npt.assert_array_equal(gt.gradients, np.reshape(bvals, (-1, 1)) * bvecs)
npt.assert_array_equal(gt.b0s_mask, [1, 0, 0, 0, 0, 0, 0, 1])
new_bvecs = bvecs.copy()
new_bvecs[[0, -1]] = np.nan
gt = gradient_table_from_bvals_bvecs(bvals, new_bvecs, b0_threshold=0)
npt.assert_array_equal(gt.bvecs, bvecs)
bad_bvals = [2, 1, 2, 3, 4, 5, 6, 0]
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
bad_bvals = np.ones(7)
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
bad_bvals = [-1, -1, -1, -5, -6, -10]
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
bad_bvals = np.ones((1, 8))
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bad_bvals, bvecs, b0_threshold=0.0)
bad_bvecs = np.ones((1, 8, 3))
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
bad_bvecs = np.ones((8, 2))
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
bad_bvecs = bvecs * 2
npt.assert_raises(ValueError, gradient_table_from_bvals_bvecs, bvals, bad_bvecs, b0_threshold=0.0)
gt = gradient_table_from_bvals_bvecs(bvals, bvecs, b0_threshold=0, big_delta=5, small_delta=2)
npt.assert_equal(gt.big_delta, 5)
npt.assert_equal(gt.small_delta, 2)
```

## Next Steps


---

*Source: test_gradients.py:268 | Complexity: Advanced | Last updated: 2026-05-18*