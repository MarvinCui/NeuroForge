# How To: Make Forward Solution Sphere

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test making a forward solution with a sphere model.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, fname_src_small
```

## Step-by-Step Guide

### Step 1: 'Test making a forward solution with a sphere model.'

```python
'Test making a forward solution with a sphere model.'
```

**Verification:**
```python
assert_allclose(np.corrcoef(fwd_['sol']['data'].ravel(), fwd_py_['sol']['data'].ravel())[0, 1], 1.0, rtol=0.001)
```

### Step 2: Assign out_name = value

```python
out_name = tmp_path / 'tmp-fwd.fif'
```

**Verification:**
```python
assert len(sphere['layers']) == 4
```

### Step 3: Call run_subprocess()

```python
run_subprocess(['mne_forward_solution', '--meg', '--eeg', '--meas', fname_raw, '--src', fname_src_small, '--mri', fname_trans, '--fwd', out_name])
```

**Verification:**
```python
assert len(sphere_1['layers']) == 0
```

### Step 4: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(out_name)
```

**Verification:**
```python
assert_array_equal(sphere['r0'], sphere_1['r0'])
```

### Step 5: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model(head_radius=0.1, relative_radii=(0.95, 0.97, 0.98, 1), verbose=True)
```

**Verification:**
```python
assert fwd['mri_head_t']['trans'][0, 3] == -0.05
```

### Step 6: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_src_small)
```

### Step 7: Assign fwd_py = make_forward_solution(...)

```python
fwd_py = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=True, verbose=True)
```

### Step 8: Call _compare_forwards()

```python
_compare_forwards(fwd, fwd_py, 366, 108, meg_rtol=0.5, meg_atol=1e-06, eeg_rtol=0.5, eeg_atol=0.5)
```

**Verification:**
```python
assert len(sphere['layers']) == 4
```

### Step 9: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
```

### Step 10: Assign sphere_1 = make_sphere_model(...)

```python
sphere_1 = make_sphere_model(head_radius=None)
```

**Verification:**
```python
assert len(sphere_1['layers']) == 0
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(sphere['r0'], sphere_1['r0'])
```

### Step 12: Assign fwd_1 = make_forward_solution(...)

```python
fwd_1 = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
```

### Step 13: Call _compare_forwards()

```python
_compare_forwards(fwd, fwd_1, 306, 108, meg_rtol=1e-12, meg_atol=1e-12)
```

### Step 14: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model(head_radius=None)
```

### Step 15: Assign custom_trans = Transform(...)

```python
custom_trans = Transform('head', 'mri')
```

### Step 16: Assign unknown = 0.05

```python
custom_trans['trans'][0, 3] = 0.05
```

### Step 17: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model()
```

### Step 18: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(fname_raw, custom_trans, src, sphere)
```

**Verification:**
```python
assert fwd['mri_head_t']['trans'][0, 3] == -0.05
```

### Step 19: Assign fwd_ = pick_types_forward(...)

```python
fwd_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
```

### Step 20: Assign fwd_py_ = pick_types_forward(...)

```python
fwd_py_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
```

### Step 21: Call assert_allclose()

```python
assert_allclose(np.corrcoef(fwd_['sol']['data'].ravel(), fwd_py_['sol']['data'].ravel())[0, 1], 1.0, rtol=0.001)
```

### Step 22: Call make_forward_solution()

```python
make_forward_solution(fname_raw, fname_trans, src, sphere)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname_src_small

# Workflow
'Test making a forward solution with a sphere model.'
out_name = tmp_path / 'tmp-fwd.fif'
run_subprocess(['mne_forward_solution', '--meg', '--eeg', '--meas', fname_raw, '--src', fname_src_small, '--mri', fname_trans, '--fwd', out_name])
fwd = read_forward_solution(out_name)
sphere = make_sphere_model(head_radius=0.1, relative_radii=(0.95, 0.97, 0.98, 1), verbose=True)
src = read_source_spaces(fname_src_small)
fwd_py = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=True, verbose=True)
_compare_forwards(fwd, fwd_py, 366, 108, meg_rtol=0.5, meg_atol=1e-06, eeg_rtol=0.5, eeg_atol=0.5)
for meg, eeg in zip([True, False], [False, True]):
    fwd_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
    fwd_py_ = pick_types_forward(fwd, meg=meg, eeg=eeg)
    assert_allclose(np.corrcoef(fwd_['sol']['data'].ravel(), fwd_py_['sol']['data'].ravel())[0, 1], 1.0, rtol=0.001)
assert len(sphere['layers']) == 4
fwd = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
sphere_1 = make_sphere_model(head_radius=None)
assert len(sphere_1['layers']) == 0
assert_array_equal(sphere['r0'], sphere_1['r0'])
fwd_1 = make_forward_solution(fname_raw, fname_trans, src, sphere, meg=True, eeg=False)
_compare_forwards(fwd, fwd_1, 306, 108, meg_rtol=1e-12, meg_atol=1e-12)
sphere = make_sphere_model(head_radius=None)
with pytest.raises(RuntimeError, match='zero shells.*EEG'):
    make_forward_solution(fname_raw, fname_trans, src, sphere)
custom_trans = Transform('head', 'mri')
custom_trans['trans'][0, 3] = 0.05
sphere = make_sphere_model()
fwd = make_forward_solution(fname_raw, custom_trans, src, sphere)
assert fwd['mri_head_t']['trans'][0, 3] == -0.05
```

## Next Steps


---

*Source: test_make_forward.py:539 | Complexity: Advanced | Last updated: 2026-05-18*