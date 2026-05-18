# How To: Carlson Rf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test carlson rf

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

### Step 1: Assign x = np.array(...)

```python
x = np.array([[1.0, 0.5], [2.0, 2.0]])
```

**Verification:**
```python
assert_array_almost_equal(RF, RF_ref)
```

### Step 2: Assign y = np.array(...)

```python
y = np.array([[2.0, 1.0], [3.0, 3.0]])
```

**Verification:**
```python
assert_array_almost_equal(RF, RF_ref)
```

### Step 3: Assign z = np.array(...)

```python
z = np.array([[0.0, 0.0], [4.0, 4.0]])
```

### Step 4: Assign RF_ref = np.array(...)

```python
RF_ref = np.array([[1.3110287771461, 1.8540746773014], [0.58408284167715, 0.58408284167715]])
```

### Step 5: Assign RF = carlson_rf(...)

```python
RF = carlson_rf(x, y, z)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RF, RF_ref)
```

### Step 7: Assign x = np.array(...)

```python
x = np.array([1j, 1j - 1, 1j, 1j - 1])
```

### Step 8: Assign y = np.array(...)

```python
y = np.array([-1j, 1j, -1j, 1j])
```

### Step 9: Assign z = np.array(...)

```python
z = np.array([0.0, 0.0, 2, 1 - 1j])
```

### Step 10: Assign RF_ref = np.array(...)

```python
RF_ref = np.array([1.8540746773014, 0.79612586584234 - 1.2138566698365j, 1.0441445654064, 0.93912050218619 - 0.53296252018635j])
```

### Step 11: Assign RF = carlson_rf(...)

```python
RF = carlson_rf(x, y, z, errtol=3e-05)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RF, RF_ref)
```


## Complete Example

```python
# Workflow
x = np.array([[1.0, 0.5], [2.0, 2.0]])
y = np.array([[2.0, 1.0], [3.0, 3.0]])
z = np.array([[0.0, 0.0], [4.0, 4.0]])
RF_ref = np.array([[1.3110287771461, 1.8540746773014], [0.58408284167715, 0.58408284167715]])
RF = carlson_rf(x, y, z)
assert_array_almost_equal(RF, RF_ref)
x = np.array([1j, 1j - 1, 1j, 1j - 1])
y = np.array([-1j, 1j, -1j, 1j])
z = np.array([0.0, 0.0, 2, 1 - 1j])
RF_ref = np.array([1.8540746773014, 0.79612586584234 - 1.2138566698365j, 1.0441445654064, 0.93912050218619 - 0.53296252018635j])
RF = carlson_rf(x, y, z, errtol=3e-05)
assert_array_almost_equal(RF, RF_ref)
```

## Next Steps


---

*Source: test_dki.py:481 | Complexity: Advanced | Last updated: 2026-05-18*