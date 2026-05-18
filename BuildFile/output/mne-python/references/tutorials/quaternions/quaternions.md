# How To: Quaternions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test quaternion calculations.

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

### Step 1: 'Test quaternion calculations.'

```python
'Test quaternion calculations.'
```

**Verification:**
```python
assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
```

### Step 2: Assign rots = value

```python
rots = [np.eye(3)]
```

**Verification:**
```python
assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
```

### Step 3: Assign y_180 = np.array(...)

```python
y_180 = np.array([[-1, 0, 0], [0, 1, 0], [0, 0, -1.0]])
```

**Verification:**
```python
assert_allclose(_angle_between_quats(a, b), expected, atol=1e-05)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(_angle_between_quats(rot_to_quat(y_180), np.zeros(3)), np.pi)
```

**Verification:**
```python
assert_allclose(_angle_between_quats(rot_to_quat(y_180), np.zeros(3)), np.pi)
```

### Step 5: Assign h_180_attitude_90 = np.array(...)

```python
h_180_attitude_90 = np.array([[0, 1, 0], [1, 0, 0], [0, 0, -1.0]])
```

**Verification:**
```python
assert_allclose(_angle_between_quats(rot_to_quat(h_180_attitude_90), np.zeros(3)), np.pi)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(_angle_between_quats(rot_to_quat(h_180_attitude_90), np.zeros(3)), np.pi)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
```

### Step 8: Assign rot = value

```python
rot = rot[np.newaxis, np.newaxis, :, :]
```

### Step 9: Call assert_allclose()

```python
assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
```

### Step 10: Assign a = np.zeros(...)

```python
a = np.zeros(3)
```

### Step 11: Assign b = np.zeros(...)

```python
b = np.zeros(3)
```

### Step 12: Assign unknown = 1.0

```python
a[ii] = 1.0
```

### Step 13: Assign unknown = 1.0

```python
b[jj] = 1.0
```

### Step 14: Assign expected = value

```python
expected = np.pi if ii != jj else 0.0
```

### Step 15: Call assert_allclose()

```python
assert_allclose(_angle_between_quats(a, b), expected, atol=1e-05)
```


## Complete Example

```python
# Workflow
'Test quaternion calculations.'
rots = [np.eye(3)]
for fname in [test_fif_fname, ctf_fname, hp_fif_fname]:
    rots += [read_info(fname)['dev_head_t']['trans'][:3, :3]]
rots += [np.array([[-0.99978541, -0.01873462, -0.00898756], [-0.01873462, 0.62565561, 0.77987608], [-0.00898756, 0.77987608, -0.62587152]])]
rots += [np.array([[0.62565561, -0.01873462, 0.77987608], [-0.01873462, -0.99978541, -0.00898756], [0.77987608, -0.00898756, -0.62587152]])]
rots += [np.array([[-0.99978541, -0.00898756, -0.01873462], [-0.00898756, -0.62587152, 0.77987608], [-0.01873462, 0.77987608, 0.62565561]])]
for rot in rots:
    assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
    rot = rot[np.newaxis, np.newaxis, :, :]
    assert_allclose(rot, quat_to_rot(rot_to_quat(rot)), rtol=1e-05, atol=1e-05)
for ii in range(3):
    for jj in range(3):
        a = np.zeros(3)
        b = np.zeros(3)
        a[ii] = 1.0
        b[jj] = 1.0
        expected = np.pi if ii != jj else 0.0
        assert_allclose(_angle_between_quats(a, b), expected, atol=1e-05)
y_180 = np.array([[-1, 0, 0], [0, 1, 0], [0, 0, -1.0]])
assert_allclose(_angle_between_quats(rot_to_quat(y_180), np.zeros(3)), np.pi)
h_180_attitude_90 = np.array([[0, 1, 0], [1, 0, 0], [0, 0, -1.0]])
assert_allclose(_angle_between_quats(rot_to_quat(h_180_attitude_90), np.zeros(3)), np.pi)
```

## Next Steps


---

*Source: test_transforms.py:324 | Complexity: Advanced | Last updated: 2026-05-18*