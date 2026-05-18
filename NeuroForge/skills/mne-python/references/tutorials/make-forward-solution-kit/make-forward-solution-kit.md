# How To: Make Forward Solution Kit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test making fwd using KIT (compensated) files.

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

### Step 1: 'Test making fwd using KIT (compensated) files.'

```python
'Test making fwd using KIT (compensated) files.'
```

**Verification:**
```python
assert isinstance(fwd, Forward)
```

### Step 2: Assign sqd_path = value

```python
sqd_path = kit_dir / 'test.sqd'
```

**Verification:**
```python
assert isinstance(fwd_py, Forward)
```

### Step 3: Assign mrk_path = value

```python
mrk_path = kit_dir / 'test_mrk.sqd'
```

**Verification:**
```python
assert 'kit_system_id' in fwd_py['info']
```

### Step 4: Assign elp_path = value

```python
elp_path = kit_dir / 'test_elp.txt'
```

### Step 5: Assign hsp_path = value

```python
hsp_path = kit_dir / 'test_hsp.txt'
```

### Step 6: Assign fname_kit_raw = value

```python
fname_kit_raw = kit_dir / 'test_bin_raw.fif'
```

### Step 7: Assign fwd = _do_forward_solution(...)

```python
fwd = _do_forward_solution('sample', fname_kit_raw, src=fname_src_small, bem=fname_bem_meg, mri=trans_path, eeg=False, meg=True, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert isinstance(fwd, Forward)
```

### Step 8: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_src_small)
```

### Step 9: Assign fwd_py = make_forward_solution(...)

```python
fwd_py = make_forward_solution(fname_kit_raw, trans_path, src, fname_bem_meg, eeg=False, meg=True)
```

### Step 10: Call _compare_forwards()

```python
_compare_forwards(fwd, fwd_py, 157, n_src_small)
```

**Verification:**
```python
assert isinstance(fwd_py, Forward)
```

### Step 11: Assign raw_py = read_raw_kit(...)

```python
raw_py = read_raw_kit(sqd_path, mrk_path, elp_path, hsp_path)
```

### Step 12: Assign meg_only_info = pick_info(...)

```python
meg_only_info = pick_info(raw_py.info, pick_types(raw_py.info, meg=True, eeg=False))
```

### Step 13: Assign fwd_py = make_forward_solution(...)

```python
fwd_py = make_forward_solution(meg_only_info, src=src, meg=True, eeg=True, bem=fname_bem_meg, trans=trans_path, ignore_ref=True)
```

### Step 14: Call _compare_forwards()

```python
_compare_forwards(fwd, fwd_py, 157, n_src_small, meg_rtol=0.001, meg_atol=1e-07)
```

**Verification:**
```python
assert 'kit_system_id' in fwd_py['info']
```

### Step 15: Call make_forward_solution()

```python
make_forward_solution(raw_py.info, src=src, eeg=False, meg=True, bem=fname_bem_meg, trans=trans_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname_src_small

# Workflow
'Test making fwd using KIT (compensated) files.'
sqd_path = kit_dir / 'test.sqd'
mrk_path = kit_dir / 'test_mrk.sqd'
elp_path = kit_dir / 'test_elp.txt'
hsp_path = kit_dir / 'test_hsp.txt'
fname_kit_raw = kit_dir / 'test_bin_raw.fif'
fwd = _do_forward_solution('sample', fname_kit_raw, src=fname_src_small, bem=fname_bem_meg, mri=trans_path, eeg=False, meg=True, subjects_dir=subjects_dir)
assert isinstance(fwd, Forward)
src = read_source_spaces(fname_src_small)
fwd_py = make_forward_solution(fname_kit_raw, trans_path, src, fname_bem_meg, eeg=False, meg=True)
_compare_forwards(fwd, fwd_py, 157, n_src_small)
assert isinstance(fwd_py, Forward)
raw_py = read_raw_kit(sqd_path, mrk_path, elp_path, hsp_path)
with pytest.raises(NotImplementedError, match='Cannot.*KIT reference'):
    make_forward_solution(raw_py.info, src=src, eeg=False, meg=True, bem=fname_bem_meg, trans=trans_path)
meg_only_info = pick_info(raw_py.info, pick_types(raw_py.info, meg=True, eeg=False))
fwd_py = make_forward_solution(meg_only_info, src=src, meg=True, eeg=True, bem=fname_bem_meg, trans=trans_path, ignore_ref=True)
_compare_forwards(fwd, fwd_py, 157, n_src_small, meg_rtol=0.001, meg_atol=1e-07)
assert 'kit_system_id' in fwd_py['info']
```

## Next Steps


---

*Source: test_make_forward.py:218 | Complexity: Advanced | Last updated: 2026-05-18*