# How To: Talxfm Rigid

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that talxfm_rigid gives reasonable results.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._freesurfer`
- `mne.datasets`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: 'Test that talxfm_rigid gives reasonable results.'

```python
'Test that talxfm_rigid gives reasonable results.'
```

**Verification:**
```python
assert_allclose(rigid, np.eye(4), atol=1e-06)
```

### Step 2: Assign rigid = _estimate_talxfm_rigid(...)

```python
rigid = _estimate_talxfm_rigid('fsaverage', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert_allclose(np.linalg.norm(rigid[:3, :3], axis=1), 1.0, atol=1e-06)
```

### Step 3: Call assert_allclose()

```python
assert_allclose(rigid, np.eye(4), atol=1e-06)
```

**Verification:**
```python
assert 30 < move < 70
```

### Step 4: Assign rigid = _estimate_talxfm_rigid(...)

```python
rigid = _estimate_talxfm_rigid('sample', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert 20 < ang < 25
```

### Step 5: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(rigid[:3, :3], axis=1), 1.0, atol=1e-06)
```

### Step 6: Assign move = value

```python
move = 1000 * np.linalg.norm(rigid[:3, 3])
```

**Verification:**
```python
assert 30 < move < 70
```

### Step 7: Assign ang = np.rad2deg(...)

```python
ang = np.rad2deg(_angle_between_quats(rot_to_quat(rigid[:3, :3])))
```

**Verification:**
```python
assert 20 < ang < 25
```


## Complete Example

```python
# Workflow
'Test that talxfm_rigid gives reasonable results.'
rigid = _estimate_talxfm_rigid('fsaverage', subjects_dir=subjects_dir)
assert_allclose(rigid, np.eye(4), atol=1e-06)
rigid = _estimate_talxfm_rigid('sample', subjects_dir=subjects_dir)
assert_allclose(np.linalg.norm(rigid[:3, :3], axis=1), 1.0, atol=1e-06)
move = 1000 * np.linalg.norm(rigid[:3, 3])
assert 30 < move < 70
ang = np.rad2deg(_angle_between_quats(rot_to_quat(rigid[:3, :3])))
assert 20 < ang < 25
```

## Next Steps


---

*Source: test_freesurfer.py:279 | Complexity: Intermediate | Last updated: 2026-05-18*