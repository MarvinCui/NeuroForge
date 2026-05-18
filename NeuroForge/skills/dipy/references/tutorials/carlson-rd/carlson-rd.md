# How To: Carlson Rd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test carlson rd

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
x = np.array([0.0, 2.0])
```

**Verification:**
```python
assert_array_almost_equal(RD, RD_ref)
```

### Step 2: Assign y = np.array(...)

```python
y = np.array([2.0, 3.0])
```

**Verification:**
```python
assert_array_almost_equal(RD, RD_ref)
```

### Step 3: Assign z = np.array(...)

```python
z = np.array([1.0, 4.0])
```

### Step 4: Assign RD_ref = np.array(...)

```python
RD_ref = np.array([1.7972103521034, 0.16510527294261])
```

### Step 5: Assign RD = carlson_rd(...)

```python
RD = carlson_rd(x, y, z, errtol=1e-05)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RD, RD_ref)
```

### Step 7: Assign x = np.array(...)

```python
x = np.array([[1j, 0.0], [0.0, -2 - 1j]])
```

### Step 8: Assign y = np.array(...)

```python
y = np.array([[-1j, 1j], [1j - 1, -1j]])
```

### Step 9: Assign z = np.array(...)

```python
z = np.array([[2.0, -1j], [1j, -1 + 1j]])
```

### Step 10: Assign RD_ref = np.array(...)

```python
RD_ref = np.array([[0.6593385415422, 1.270819627191 + 2.7811120159521j], [-1.8577235439239 - 0.96193450888839j, 1.8249027393704 - 1.2218475784827j]])
```

### Step 11: Assign RD = carlson_rd(...)

```python
RD = carlson_rd(x, y, z, errtol=1e-05)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RD, RD_ref)
```


## Complete Example

```python
# Workflow
x = np.array([0.0, 2.0])
y = np.array([2.0, 3.0])
z = np.array([1.0, 4.0])
RD_ref = np.array([1.7972103521034, 0.16510527294261])
RD = carlson_rd(x, y, z, errtol=1e-05)
assert_array_almost_equal(RD, RD_ref)
x = np.array([[1j, 0.0], [0.0, -2 - 1j]])
y = np.array([[-1j, 1j], [1j - 1, -1j]])
z = np.array([[2.0, -1j], [1j, -1 + 1j]])
RD_ref = np.array([[0.6593385415422, 1.270819627191 + 2.7811120159521j], [-1.8577235439239 - 0.96193450888839j, 1.8249027393704 - 1.2218475784827j]])
RD = carlson_rd(x, y, z, errtol=1e-05)
assert_array_almost_equal(RD, RD_ref)
```

## Next Steps


---

*Source: test_dki.py:523 | Complexity: Advanced | Last updated: 2026-05-18*