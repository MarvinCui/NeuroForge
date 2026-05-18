# How To: Average Quats

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test averaging of quaternions.

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

### Step 1: 'Test averaging of quaternions.'

```python
'Test averaging of quaternions.'
```

**Verification:**
```python
assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
```

### Step 2: Assign sq2 = value

```python
sq2 = 1.0 / np.sqrt(2.0)
```

**Verification:**
```python
assert_allclose(rot_0, rot_1, atol=1e-07)
```

### Step 3: Assign quats = np.array(...)

```python
quats = np.array([[0, sq2, sq2], [0, sq2, sq2], [0, sq2, 0], [0, 0, sq2], [sq2, 0, 0]], float)
```

**Verification:**
```python
assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
```

### Step 4: Assign expected = value

```python
expected = [quats[0], quats[0], [0, 0.788675134594813, 0.577350269189626], [0, 0.657192299694123, 0.657192299694123], [0.10040605854054, 0.616329446922803, 0.616329446922803]]
```

**Verification:**
```python
assert_allclose(angle, 0.0, atol=1e-07)
```

### Step 5: Assign unknown = quat_to_rot(...)

```python
rot_0, rot_1 = quat_to_rot(quats[:2])
```

**Verification:**
```python
assert_allclose(rot_0, rot_1, atol=1e-07)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(rot_0, rot_1, atol=1e-07)
```

**Verification:**
```python
assert count == 4 + len(extras)
```

### Step 7: Assign count = 0

```python
count = 0
```

### Step 8: Assign extras = value

```python
extras = [[sq2, sq2, 0]] + list(np.eye(3))
```

**Verification:**
```python
assert count == 4 + len(extras)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
```

### Step 11: Assign angle = _angle_between_quats(...)

```python
angle = _angle_between_quats(quat, -quat)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(angle, 0.0, atol=1e-07)
```

### Step 13: Assign unknown = quat_to_rot(...)

```python
rot_0, rot_1 = quat_to_rot(np.array((quat, -quat)))
```

### Step 14: Call assert_allclose()

```python
assert_allclose(rot_0, rot_1, atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test averaging of quaternions.'
sq2 = 1.0 / np.sqrt(2.0)
quats = np.array([[0, sq2, sq2], [0, sq2, sq2], [0, sq2, 0], [0, 0, sq2], [sq2, 0, 0]], float)
expected = [quats[0], quats[0], [0, 0.788675134594813, 0.577350269189626], [0, 0.657192299694123, 0.657192299694123], [0.10040605854054, 0.616329446922803, 0.616329446922803]]
for lim, ex in enumerate(expected):
    assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
quats[1] *= -1
rot_0, rot_1 = quat_to_rot(quats[:2])
assert_allclose(rot_0, rot_1, atol=1e-07)
for lim, ex in enumerate(expected):
    assert_allclose(_average_quats(quats[:lim + 1]), ex, atol=1e-07)
count = 0
extras = [[sq2, sq2, 0]] + list(np.eye(3))
for quat in np.concatenate((quats, expected, extras)):
    if np.isclose(_quat_real(quat), 0.0, atol=1e-07):
        count += 1
        angle = _angle_between_quats(quat, -quat)
        assert_allclose(angle, 0.0, atol=1e-07)
        rot_0, rot_1 = quat_to_rot(np.array((quat, -quat)))
        assert_allclose(rot_0, rot_1, atol=1e-07)
assert count == 4 + len(extras)
```

## Next Steps


---

*Source: test_transforms.py:391 | Complexity: Advanced | Last updated: 2026-05-18*