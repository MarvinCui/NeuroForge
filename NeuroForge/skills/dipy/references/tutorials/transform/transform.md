# How To: Transform

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transform

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `dipy.nn.utils`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign temp = rng.random(...)

```python
temp = rng.random((28, 30, 34))
```

### Step 2: Assign unknown = transform_img(...)

```python
temp2, params = transform_img(temp, np.eye(4), target_voxsize=tuple(np.ones(3) * 2), final_size=(14, 15, 16))
```

### Step 3: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(np.array(temp.shape), np.array(temp2.shape))
```

### Step 4: Assign scipy_affine_txfm_msg = 'The behavior of affine_transform with a 1-D array supplied for the matrix parameter has changed in SciPy 0.18.0.'

```python
scipy_affine_txfm_msg = 'The behavior of affine_transform with a 1-D array supplied for the matrix parameter has changed in SciPy 0.18.0.'
```

### Step 5: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=scipy_affine_txfm_msg, category=UserWarning)
```

### Step 6: Assign temp2 = recover_img(...)

```python
temp2 = recover_img(temp2, params)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
temp = rng.random((28, 30, 34))
temp2, params = transform_img(temp, np.eye(4), target_voxsize=tuple(np.ones(3) * 2), final_size=(14, 15, 16))
with warnings.catch_warnings():
    scipy_affine_txfm_msg = 'The behavior of affine_transform with a 1-D array supplied for the matrix parameter has changed in SciPy 0.18.0.'
    warnings.filterwarnings('ignore', message=scipy_affine_txfm_msg, category=UserWarning)
    temp2 = recover_img(temp2, params)
np.testing.assert_almost_equal(np.array(temp.shape), np.array(temp2.shape))
```

## Next Steps


---

*Source: test_utils.py:18 | Complexity: Intermediate | Last updated: 2026-05-18*