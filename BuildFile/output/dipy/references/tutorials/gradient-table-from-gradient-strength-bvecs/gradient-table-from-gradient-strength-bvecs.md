# How To: Gradient Table From Gradient Strength Bvecs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gradient table from gradient strength bvecs

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

### Step 1: Assign gradient_strength = value

```python
gradient_strength = 3e-05 * np.ones(7)
```

### Step 2: Assign big_delta = 0.03

```python
big_delta = 0.03
```

### Step 3: Assign small_delta = 0.01

```python
small_delta = 0.01
```

### Step 4: Assign unknown = 0

```python
gradient_strength[0] = 0
```

### Step 5: Assign sq2 = value

```python
sq2 = np.sqrt(2) / 2
```

### Step 6: Assign bvecs = np.array(...)

```python
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
```

### Step 7: Assign gt = gradient_table_from_gradient_strength_bvecs(...)

```python
gt = gradient_table_from_gradient_strength_bvecs(gradient_strength, bvecs, big_delta, small_delta)
```

### Step 8: Assign qvals_expected = value

```python
qvals_expected = gradient_strength * WATER_GYROMAGNETIC_RATIO * small_delta / (2 * np.pi)
```

### Step 9: Assign bvals_expected = value

```python
bvals_expected = (qvals_expected * 2 * np.pi) ** 2 * (big_delta - small_delta / 3.0)
```

### Step 10: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(gt.qvals, qvals_expected)
```

### Step 11: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(gt.bvals, bvals_expected)
```


## Complete Example

```python
# Workflow
gradient_strength = 3e-05 * np.ones(7)
big_delta = 0.03
small_delta = 0.01
gradient_strength[0] = 0
sq2 = np.sqrt(2) / 2
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
gt = gradient_table_from_gradient_strength_bvecs(gradient_strength, bvecs, big_delta, small_delta)
qvals_expected = gradient_strength * WATER_GYROMAGNETIC_RATIO * small_delta / (2 * np.pi)
bvals_expected = (qvals_expected * 2 * np.pi) ** 2 * (big_delta - small_delta / 3.0)
npt.assert_almost_equal(gt.qvals, qvals_expected)
npt.assert_almost_equal(gt.bvals, bvals_expected)
```

## Next Steps


---

*Source: test_gradients.py:240 | Complexity: Advanced | Last updated: 2026-05-18*