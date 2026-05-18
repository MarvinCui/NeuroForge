# How To: Rotation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test conversion between rotation angles and transformation matrix.

## Prerequisites

**Required Modules:**
- `itertools`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.transforms`
- `mne.transforms`
- `dipy.align`


## Step-by-Step Guide

### Step 1: 'Test conversion between rotation angles and transformation matrix.'

```python
'Test conversion between rotation angles and transformation matrix.'
```

**Verification:**
```python
assert_array_equal(m, m4[:3, :3])
```

### Step 2: Assign tests = value

```python
tests = [(0, 0, 1), (0.5, 0.5, 0.5), (np.pi, 0, -1.5)]
```

**Verification:**
```python
assert_almost_equal(actual=back, desired=rot, decimal=12)
```

### Step 3: Assign unknown = rot

```python
x, y, z = rot
```

**Verification:**
```python
assert_almost_equal(actual=back4, desired=rot, decimal=12)
```

### Step 4: Assign m = rotation3d(...)

```python
m = rotation3d(x, y, z)
```

### Step 5: Assign m4 = rotation(...)

```python
m4 = rotation(x, y, z)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(m, m4[:3, :3])
```

### Step 7: Assign back = rotation_angles(...)

```python
back = rotation_angles(m)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(actual=back, desired=rot, decimal=12)
```

### Step 9: Assign back4 = rotation_angles(...)

```python
back4 = rotation_angles(m4)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(actual=back4, desired=rot, decimal=12)
```


## Complete Example

```python
# Workflow
'Test conversion between rotation angles and transformation matrix.'
tests = [(0, 0, 1), (0.5, 0.5, 0.5), (np.pi, 0, -1.5)]
for rot in tests:
    x, y, z = rot
    m = rotation3d(x, y, z)
    m4 = rotation(x, y, z)
    assert_array_equal(m, m4[:3, :3])
    back = rotation_angles(m)
    assert_almost_equal(actual=back, desired=rot, decimal=12)
    back4 = rotation_angles(m4)
    assert_almost_equal(actual=back4, desired=rot, decimal=12)
```

## Next Steps


---

*Source: test_transforms.py:265 | Complexity: Advanced | Last updated: 2026-05-18*