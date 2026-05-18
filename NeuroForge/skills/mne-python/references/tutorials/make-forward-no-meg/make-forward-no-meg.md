# How To: Make Forward No Meg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can make and I/O forward solution with no MEG channels.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that we can make and I/O forward solution with no MEG channels.'

```python
'Test that we can make and I/O forward solution with no MEG channels.'
```

**Verification:**
```python
assert info['dev_head_t'] is None
```

### Step 2: Assign pos = dict(...)

```python
pos = dict(rr=[[0.05, 0, 0]], nn=[[0, 0, 1.0]])
```

**Verification:**
```python
assert fwd['info']['dev_head_t'] is None
```

### Step 3: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(pos=pos)
```

**Verification:**
```python
assert_allclose(fwd['sol']['data'], fwd_read['sol']['data'])
```

### Step 4: Assign bem = make_sphere_model(...)

```python
bem = make_sphere_model()
```

**Verification:**
```python
assert fwd_read['info']['dev_head_t'] is None
```

### Step 5: Assign trans = None

```python
trans = None
```

### Step 6: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage('standard_1020')
```

### Step 7: Assign info = create_info.set_montage(...)

```python
info = create_info(['Cz'], 1000.0, 'eeg').set_montage(montage)
```

**Verification:**
```python
assert info['dev_head_t'] is None
```

### Step 8: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(info, trans, src, bem)
```

**Verification:**
```python
assert fwd['info']['dev_head_t'] is None
```

### Step 9: Assign fname = value

```python
fname = tmp_path / 'test-fwd.fif'
```

### Step 10: Call write_forward_solution()

```python
write_forward_solution(fname, fwd)
```

### Step 11: Assign fwd_read = read_forward_solution(...)

```python
fwd_read = read_forward_solution(fname)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(fwd['sol']['data'], fwd_read['sol']['data'])
```

**Verification:**
```python
assert fwd_read['info']['dev_head_t'] is None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that we can make and I/O forward solution with no MEG channels.'
pos = dict(rr=[[0.05, 0, 0]], nn=[[0, 0, 1.0]])
src = setup_volume_source_space(pos=pos)
bem = make_sphere_model()
trans = None
montage = make_standard_montage('standard_1020')
info = create_info(['Cz'], 1000.0, 'eeg').set_montage(montage)
assert info['dev_head_t'] is None
fwd = make_forward_solution(info, trans, src, bem)
assert fwd['info']['dev_head_t'] is None
fname = tmp_path / 'test-fwd.fif'
write_forward_solution(fname, fwd)
fwd_read = read_forward_solution(fname)
assert_allclose(fwd['sol']['data'], fwd_read['sol']['data'])
assert fwd_read['info']['dev_head_t'] is None
```

## Next Steps


---

*Source: test_make_forward.py:831 | Complexity: Advanced | Last updated: 2026-05-18*