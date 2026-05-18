# How To: Set Montage Artinis Fsaverage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that artinis montages match fsaverage's head<->MRI transform.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.montage`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: kind
```

## Step-by-Step Guide

### Step 1: "Test that artinis montages match fsaverage's head<->MRI transform."

```python
"Test that artinis montages match fsaverage's head<->MRI transform."
```

**Verification:**
```python
assert trans['to'] == trans_fs['to']
```

### Step 2: Assign unknown = _get_trans(...)

```python
trans_fs, _ = _get_trans('fsaverage')
```

**Verification:**
```python
assert trans['from'] == trans_fs['from']
```

### Step 3: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage(f'artinis-{kind}')
```

**Verification:**
```python
assert 0 < translation < 1
```

### Step 4: Assign trans = compute_native_head_t(...)

```python
trans = compute_native_head_t(montage)
```

**Verification:**
```python
assert 0 < rotation < 1
```

### Step 5: Assign translation = value

```python
translation = 1000 * np.linalg.norm(trans['trans'][:3, 3] - trans_fs['trans'][:3, 3])
```

**Verification:**
```python
assert 0 < translation < 1
```

### Step 6: Assign rotation = np.rad2deg(...)

```python
rotation = np.rad2deg(_angle_between_quats(rot_to_quat(trans['trans'][:3, :3]), rot_to_quat(trans_fs['trans'][:3, :3])))
```

**Verification:**
```python
assert 0 < rotation < 1
```


## Complete Example

```python
# Setup
# Fixtures: kind

# Workflow
"Test that artinis montages match fsaverage's head<->MRI transform."
trans_fs, _ = _get_trans('fsaverage')
montage = make_standard_montage(f'artinis-{kind}')
trans = compute_native_head_t(montage)
assert trans['to'] == trans_fs['to']
assert trans['from'] == trans_fs['from']
translation = 1000 * np.linalg.norm(trans['trans'][:3, 3] - trans_fs['trans'][:3, 3])
assert 0 < translation < 1
rotation = np.rad2deg(_angle_between_quats(rot_to_quat(trans['trans'][:3, :3]), rot_to_quat(trans_fs['trans'][:3, :3])))
assert 0 < rotation < 1
```

## Next Steps


---

*Source: test_standard_montage.py:171 | Complexity: Intermediate | Last updated: 2026-05-18*