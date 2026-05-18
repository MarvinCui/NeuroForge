# How To: Vector Rotation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test basic rotation matrix math.

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

### Step 1: 'Test basic rotation matrix math.'

```python
'Test basic rotation matrix math.'
```

**Verification:**
```python
assert_array_equal(rot, [[0, -1, 0], [1, 0, 0], [0, 0, 1]])
```

### Step 2: Assign x = np.array(...)

```python
x = np.array([1.0, 0.0, 0.0])
```

**Verification:**
```python
assert_allclose(_angle_between_quats(quat_1, quat_2), np.pi / 2.0)
```

### Step 3: Assign y = np.array(...)

```python
y = np.array([0.0, 1.0, 0.0])
```

### Step 4: Assign rot = _find_vector_rotation(...)

```python
rot = _find_vector_rotation(x, y)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(rot, [[0, -1, 0], [1, 0, 0], [0, 0, 1]])
```

### Step 6: Assign quat_1 = rot_to_quat(...)

```python
quat_1 = rot_to_quat(rot)
```

### Step 7: Assign quat_2 = rot_to_quat(...)

```python
quat_2 = rot_to_quat(np.eye(3))
```

### Step 8: Call assert_allclose()

```python
assert_allclose(_angle_between_quats(quat_1, quat_2), np.pi / 2.0)
```


## Complete Example

```python
# Workflow
'Test basic rotation matrix math.'
x = np.array([1.0, 0.0, 0.0])
y = np.array([0.0, 1.0, 0.0])
rot = _find_vector_rotation(x, y)
assert_array_equal(rot, [[0, -1, 0], [1, 0, 0], [0, 0, 1]])
quat_1 = rot_to_quat(rot)
quat_2 = rot_to_quat(np.eye(3))
assert_allclose(_angle_between_quats(quat_1, quat_2), np.pi / 2.0)
```

## Next Steps


---

*Source: test_transforms.py:380 | Complexity: Advanced | Last updated: 2026-05-18*