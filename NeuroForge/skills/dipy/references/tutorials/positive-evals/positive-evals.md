# How To: Positive Evals

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test positive evals

## Prerequisites

**Required Modules:**
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dki`
- `dipy.reconst.dki`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.utils`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`


## Step-by-Step Guide

### Step 1: Assign L1 = np.array(...)

```python
L1 = np.array([[0.001, 0.001, 0.002], [0, 0.001, 0]])
```

**Verification:**
```python
assert_array_equal(ind, expected_ind)
```

### Step 2: Assign L2 = np.array(...)

```python
L2 = np.array([[0.003, 0, 0.002], [0.001, 0.001, 0]])
```

### Step 3: Assign L3 = np.array(...)

```python
L3 = np.array([[0.004, 0.0001, 0], [0, 0.001, 0]])
```

### Step 4: Assign expected_ind = np.array(...)

```python
expected_ind = np.array([[True, False, False], [False, True, False]], dtype=bool)
```

### Step 5: Assign ind = _positive_evals(...)

```python
ind = _positive_evals(L1, L2, L3)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(ind, expected_ind)
```


## Complete Example

```python
# Workflow
L1 = np.array([[0.001, 0.001, 0.002], [0, 0.001, 0]])
L2 = np.array([[0.003, 0, 0.002], [0.001, 0.001, 0]])
L3 = np.array([[0.004, 0.0001, 0], [0, 0.001, 0]])
expected_ind = np.array([[True, False, False], [False, True, False]], dtype=bool)
ind = _positive_evals(L1, L2, L3)
assert_array_equal(ind, expected_ind)
```

## Next Steps


---

*Source: test_dki.py:142 | Complexity: Intermediate | Last updated: 2026-05-18*