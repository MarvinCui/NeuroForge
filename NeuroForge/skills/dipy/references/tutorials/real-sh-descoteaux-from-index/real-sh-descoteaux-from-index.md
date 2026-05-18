# How To: Real Sh Descoteaux From Index

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test real sh descoteaux from index

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.interpolation`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign rsh = real_sh_descoteaux_from_index

```python
rsh = real_sh_descoteaux_from_index
```

**Verification:**
```python
assert_array_almost_equal(rsh(0, 0, 0, 0), 0.5 / sqrt(pi))
```

### Step 2: Assign pi = value

```python
pi = np.pi
```

**Verification:**
```python
assert_array_almost_equal(rsh(-2, 2, pi / 5, pi / 3), 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * cos(0 + 2.0 * pi / 3) * sqrt(2))
```

### Step 3: Assign sqrt = value

```python
sqrt = np.sqrt
```

**Verification:**
```python
assert_array_almost_equal(rsh(2, 2, pi / 5, pi / 3), -1 * 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * sin(0 - 2.0 * pi / 3) * sqrt(2))
```

### Step 4: Assign sin = value

```python
sin = np.sin
```

**Verification:**
```python
assert_array_almost_equal(rsh(-2, 2, pi / 2, pi), 0.25 * sqrt(15 / (2.0 * pi)) * cos(2.0 * pi) * sin(pi / 2.0) ** 2.0 * sqrt(2))
```

### Step 5: Assign cos = value

```python
cos = np.cos
```

**Verification:**
```python
assert_array_almost_equal(rsh(2, 4, pi / 3.0, pi / 4.0), -1 * (3.0 / 8.0) * sqrt(5.0 / (2.0 * pi)) * sin(0 - 2.0 * pi / 4.0) * sin(pi / 3.0) ** 2.0 * (7.0 * cos(pi / 3.0) ** 2.0 - 1) * sqrt(2))
```

### Step 6: Assign aa = np.ones(...)

```python
aa = np.ones((3, 1, 1, 1))
```

**Verification:**
```python
assert_array_almost_equal(rsh(-4, 4, pi / 6.0, pi / 8.0), 3.0 / 16.0 * sqrt(35.0 / (2.0 * pi)) * cos(0 + 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
```

### Step 7: Assign bb = np.ones(...)

```python
bb = np.ones((1, 4, 1, 1))
```

**Verification:**
```python
assert_array_almost_equal(rsh(4, 4, pi / 6.0, pi / 8.0), -1 * (3.0 / 16.0) * sqrt(35.0 / (2.0 * pi)) * sin(0 - 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
```

### Step 8: Assign cc = np.ones(...)

```python
cc = np.ones((1, 1, 5, 1))
```

**Verification:**
```python
assert_equal(rsh(aa, bb, cc, dd).shape, (3, 4, 5, 6))
```

### Step 9: Assign dd = np.ones(...)

```python
dd = np.ones((1, 1, 1, 6))
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(0, 0, 0, 0), 0.5 / sqrt(pi))
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(-2, 2, pi / 5, pi / 3), 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * cos(0 + 2.0 * pi / 3) * sqrt(2))
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(2, 2, pi / 5, pi / 3), -1 * 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * sin(0 - 2.0 * pi / 3) * sqrt(2))
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(-2, 2, pi / 2, pi), 0.25 * sqrt(15 / (2.0 * pi)) * cos(2.0 * pi) * sin(pi / 2.0) ** 2.0 * sqrt(2))
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(2, 4, pi / 3.0, pi / 4.0), -1 * (3.0 / 8.0) * sqrt(5.0 / (2.0 * pi)) * sin(0 - 2.0 * pi / 4.0) * sin(pi / 3.0) ** 2.0 * (7.0 * cos(pi / 3.0) ** 2.0 - 1) * sqrt(2))
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(-4, 4, pi / 6.0, pi / 8.0), 3.0 / 16.0 * sqrt(35.0 / (2.0 * pi)) * cos(0 + 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rsh(4, 4, pi / 6.0, pi / 8.0), -1 * (3.0 / 16.0) * sqrt(35.0 / (2.0 * pi)) * sin(0 - 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
```

### Step 18: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 19: Call assert_equal()

```python
assert_equal(rsh(aa, bb, cc, dd).shape, (3, 4, 5, 6))
```


## Complete Example

```python
# Workflow
rsh = real_sh_descoteaux_from_index
pi = np.pi
sqrt = np.sqrt
sin = np.sin
cos = np.cos
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    assert_array_almost_equal(rsh(0, 0, 0, 0), 0.5 / sqrt(pi))
    assert_array_almost_equal(rsh(-2, 2, pi / 5, pi / 3), 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * cos(0 + 2.0 * pi / 3) * sqrt(2))
    assert_array_almost_equal(rsh(2, 2, pi / 5, pi / 3), -1 * 0.25 * sqrt(15.0 / (2.0 * pi)) * sin(pi / 5.0) ** 2.0 * sin(0 - 2.0 * pi / 3) * sqrt(2))
    assert_array_almost_equal(rsh(-2, 2, pi / 2, pi), 0.25 * sqrt(15 / (2.0 * pi)) * cos(2.0 * pi) * sin(pi / 2.0) ** 2.0 * sqrt(2))
    assert_array_almost_equal(rsh(2, 4, pi / 3.0, pi / 4.0), -1 * (3.0 / 8.0) * sqrt(5.0 / (2.0 * pi)) * sin(0 - 2.0 * pi / 4.0) * sin(pi / 3.0) ** 2.0 * (7.0 * cos(pi / 3.0) ** 2.0 - 1) * sqrt(2))
    assert_array_almost_equal(rsh(-4, 4, pi / 6.0, pi / 8.0), 3.0 / 16.0 * sqrt(35.0 / (2.0 * pi)) * cos(0 + 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
    assert_array_almost_equal(rsh(4, 4, pi / 6.0, pi / 8.0), -1 * (3.0 / 16.0) * sqrt(35.0 / (2.0 * pi)) * sin(0 - 4.0 * pi / 8.0) * sin(pi / 6.0) ** 4.0 * sqrt(2))
aa = np.ones((3, 1, 1, 1))
bb = np.ones((1, 4, 1, 1))
cc = np.ones((1, 1, 5, 1))
dd = np.ones((1, 1, 1, 6))
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    assert_equal(rsh(aa, bb, cc, dd).shape, (3, 4, 5, 6))
```

## Next Steps


---

*Source: test_shm.py:107 | Complexity: Advanced | Last updated: 2026-05-18*