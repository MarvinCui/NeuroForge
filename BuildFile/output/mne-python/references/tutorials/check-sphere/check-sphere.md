# How To: Check Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the _check_sphere function.

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.utils`
- `types`


## Step-by-Step Guide

### Step 1: 'Test the _check_sphere function.'

```python
'Test the _check_sphere function.'
```

**Verification:**
```python
assert_equal(_check_sphere(None), [0, 0, 0, 0.095])
```

### Step 2: Assign info = mne.io.read_info(...)

```python
info = mne.io.read_info(fname_raw)
```

**Verification:**
```python
assert not np.any(_check_sphere(None, info) == 0)
```

### Step 3: Assign info_eeglab = create_info(...)

```python
info_eeglab = create_info(ch_names=['Fpz', 'Oz', 'T7', 'T8'], sfreq=100, ch_types='eeg')
```

**Verification:**
```python
assert_equal(_check_sphere([1, 2, 3, 4], info), [1, 2, 3, 4])
```

### Step 4: Call info_eeglab.set_montage()

```python
info_eeglab.set_montage('biosemi64')
```

**Verification:**
```python
assert_equal(_check_sphere([1, 2, 3, 4], info=None), [1, 2, 3, 4])
```

### Step 5: Call assert_equal()

```python
assert_equal(_check_sphere(None), [0, 0, 0, 0.095])
```

**Verification:**
```python
assert_allclose(sphere_auto, sphere_extra)
```

### Step 6: Call assert_equal()

```python
assert_equal(_check_sphere([1, 2, 3, 4], info), [1, 2, 3, 4])
```

**Verification:**
```python
assert not np.allclose(sphere_auto, sphere_eeglab, rtol=0.0001, atol=0.0001)
```

### Step 7: Call assert_equal()

```python
assert_equal(_check_sphere([1, 2, 3, 4], info=None), [1, 2, 3, 4])
```

**Verification:**
```python
assert not np.allclose(sphere_auto, sphere_eeg, rtol=0.0001, atol=0.0001)
```

### Step 8: Assign sphere_auto = _check_sphere(...)

```python
sphere_auto = _check_sphere('auto', info)
```

**Verification:**
```python
assert not np.allclose(sphere_auto, sphere_hpi, rtol=0.0001, atol=0.0001)
```

### Step 9: Assign sphere_eeglab = _check_sphere(...)

```python
sphere_eeglab = _check_sphere('eeglab', info_eeglab)
```

**Verification:**
```python
assert not np.allclose(sphere_auto, sphere_all, rtol=0.0001, atol=0.0001)
```

### Step 10: Assign sphere_extra = _check_sphere(...)

```python
sphere_extra = _check_sphere('extra', info)
```

### Step 11: Assign sphere_eeg = _check_sphere(...)

```python
sphere_eeg = _check_sphere('eeg', info)
```

### Step 12: Assign sphere_all = _check_sphere(...)

```python
sphere_all = _check_sphere(['extra', 'eeg', 'cardinal', 'hpi'], info)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(sphere_auto, sphere_extra)
```

**Verification:**
```python
assert not np.allclose(sphere_auto, sphere_eeglab, rtol=0.0001, atol=0.0001)
```

### Step 14: Assign info_trunc = info.copy(...)

```python
info_trunc = info.copy()
```

### Step 15: Call _check_sphere()

```python
_check_sphere([1, 2, 3], info)
```

### Step 16: Assign sphere_hpi = _check_sphere(...)

```python
sphere_hpi = _check_sphere('hpi', info)
```

### Step 17: Call _check_sphere()

```python
_check_sphere('auto', info=None)
```

### Step 18: Assign unknown = value

```python
info_trunc['dig'] = info_trunc['dig'][:20]
```

### Step 19: Call _check_sphere()

```python
_check_sphere('auto', info_trunc)
```

### Step 20: Call _check_sphere()

```python
_check_sphere('auto', info_trunc)
```


## Complete Example

```python
# Workflow
'Test the _check_sphere function.'
info = mne.io.read_info(fname_raw)
info_eeglab = create_info(ch_names=['Fpz', 'Oz', 'T7', 'T8'], sfreq=100, ch_types='eeg')
info_eeglab.set_montage('biosemi64')
assert_equal(_check_sphere(None), [0, 0, 0, 0.095])
assert not np.any(_check_sphere(None, info) == 0)
assert_equal(_check_sphere([1, 2, 3, 4], info), [1, 2, 3, 4])
assert_equal(_check_sphere([1, 2, 3, 4], info=None), [1, 2, 3, 4])
with pytest.raises(ValueError, match='1D array of shape \\(4,\\)'):
    _check_sphere([1, 2, 3], info)
sphere_auto = _check_sphere('auto', info)
sphere_eeglab = _check_sphere('eeglab', info_eeglab)
sphere_extra = _check_sphere('extra', info)
sphere_eeg = _check_sphere('eeg', info)
with _record_warnings(), pytest.warns(RuntimeWarning, match='may be inaccurate'):
    sphere_hpi = _check_sphere('hpi', info)
sphere_all = _check_sphere(['extra', 'eeg', 'cardinal', 'hpi'], info)
assert_allclose(sphere_auto, sphere_extra)
assert not np.allclose(sphere_auto, sphere_eeglab, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_eeg, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_hpi, rtol=0.0001, atol=0.0001)
assert not np.allclose(sphere_auto, sphere_all, rtol=0.0001, atol=0.0001)
with pytest.raises(TypeError, match='Item must be an instance of Info'):
    _check_sphere('auto', info=None)
info_trunc = info.copy()
with info_trunc._unlock():
    info_trunc['dig'] = info_trunc['dig'][:20]
with _record_warnings(), pytest.warns(RuntimeWarning, match='may be inaccurate'):
    _check_sphere('auto', info_trunc)
with mne.use_log_level('error'):
    _check_sphere('auto', info_trunc)
```

## Next Steps


---

*Source: test_check.py:387 | Complexity: Advanced | Last updated: 2026-05-18*