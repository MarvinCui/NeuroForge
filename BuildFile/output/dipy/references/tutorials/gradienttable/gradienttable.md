# How To: Gradienttable

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test GradientTable

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

### Step 1: Assign gradients = np.array(...)

```python
gradients = np.array([[0, 0, 0], [1, 0, 0], [0, 0, 1], [3, 4, 0], [5, 0, 12]], 'float')
```

**Verification:**
```python
assert len(selected_w) >= 1
```

### Step 2: Assign expected_bvals = np.array(...)

```python
expected_bvals = np.array([0, 1, 1, 5, 13])
```

### Step 3: Assign expected_b0s_mask = value

```python
expected_b0s_mask = expected_bvals == 0
```

### Step 4: Assign expected_bvecs = value

```python
expected_bvecs = gradients / (expected_bvals + expected_b0s_mask)[:, None]
```

### Step 5: Assign gt = GradientTable(...)

```python
gt = GradientTable(gradients, b0_threshold=0)
```

### Step 6: Call npt.assert_()

```python
npt.assert_('B-values shape (5,)' in gt.__str__())
```

### Step 7: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(gt.bvals, expected_bvals)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.b0s_mask, expected_b0s_mask)
```

### Step 9: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(gt.bvecs, expected_bvecs)
```

### Step 10: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(gt.gradients, gradients)
```

### Step 11: Assign gt = GradientTable(...)

```python
gt = GradientTable(gradients, b0_threshold=1)
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.b0s_mask, [1, 1, 1, 0, 0])
```

### Step 13: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.bvals, expected_bvals)
```

### Step 14: Call npt.assert_array_equal()

```python
npt.assert_array_equal(gt.bvecs, expected_bvecs)
```

### Step 15: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, GradientTable, -1)
```

### Step 16: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, GradientTable, np.ones((6, 2)))
```

### Step 17: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, GradientTable, np.ones((6,)))
```

### Step 18: Assign _ = gradient_table(...)

```python
_ = gradient_table(expected_bvals, bvecs=expected_bvecs, b0_threshold=200)
```

### Step 19: Assign selected_w = value

```python
selected_w = [w for w in l_warns if issubclass(w.category, UserWarning)]
```

**Verification:**
```python
assert len(selected_w) >= 1
```

### Step 20: Assign msg = value

```python
msg = [str(m.message) for m in selected_w]
```

### Step 21: Call npt.assert_equal()

```python
npt.assert_equal('b0_threshold has a value > 199' in msg, True)
```


## Complete Example

```python
# Workflow
gradients = np.array([[0, 0, 0], [1, 0, 0], [0, 0, 1], [3, 4, 0], [5, 0, 12]], 'float')
expected_bvals = np.array([0, 1, 1, 5, 13])
expected_b0s_mask = expected_bvals == 0
expected_bvecs = gradients / (expected_bvals + expected_b0s_mask)[:, None]
gt = GradientTable(gradients, b0_threshold=0)
npt.assert_('B-values shape (5,)' in gt.__str__())
npt.assert_array_almost_equal(gt.bvals, expected_bvals)
npt.assert_array_equal(gt.b0s_mask, expected_b0s_mask)
npt.assert_array_almost_equal(gt.bvecs, expected_bvecs)
npt.assert_array_almost_equal(gt.gradients, gradients)
gt = GradientTable(gradients, b0_threshold=1)
npt.assert_array_equal(gt.b0s_mask, [1, 1, 1, 0, 0])
npt.assert_array_equal(gt.bvals, expected_bvals)
npt.assert_array_equal(gt.bvecs, expected_bvecs)
npt.assert_raises(ValueError, GradientTable, -1)
npt.assert_raises(ValueError, GradientTable, np.ones((6, 2)))
npt.assert_raises(ValueError, GradientTable, np.ones((6,)))
with warnings.catch_warnings(record=True) as l_warns:
    _ = gradient_table(expected_bvals, bvecs=expected_bvecs, b0_threshold=200)
    selected_w = [w for w in l_warns if issubclass(w.category, UserWarning)]
    assert len(selected_w) >= 1
    msg = [str(m.message) for m in selected_w]
    npt.assert_equal('b0_threshold has a value > 199' in msg, True)
```

## Next Steps


---

*Source: test_gradients.py:94 | Complexity: Advanced | Last updated: 2026-05-18*