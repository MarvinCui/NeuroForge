# How To: Make Forward Solution Bti

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test BTI end-to-end versus C.

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
# Fixtures: fname_src_small
```

## Step-by-Step Guide

### Step 1: 'Test BTI end-to-end versus C.'

```python
'Test BTI end-to-end versus C.'
```

### Step 2: Assign bti_pdf = value

```python
bti_pdf = bti_dir / 'test_pdf_linux'
```

### Step 3: Assign bti_config = value

```python
bti_config = bti_dir / 'test_config_linux'
```

### Step 4: Assign bti_hs = value

```python
bti_hs = bti_dir / 'test_hs_linux'
```

### Step 5: Assign fname_bti_raw = value

```python
fname_bti_raw = bti_dir / 'exported4D_linux_raw.fif'
```

### Step 6: Assign raw_py = read_raw_bti(...)

```python
raw_py = read_raw_bti(bti_pdf, bti_config, bti_hs, preload=False)
```

### Step 7: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_src_small)
```

### Step 8: Assign fwd_py = make_forward_solution(...)

```python
fwd_py = make_forward_solution(raw_py.info, src=src, eeg=False, meg=True, bem=fname_bem_meg, trans=trans_path)
```

### Step 9: Assign fwd = _do_forward_solution(...)

```python
fwd = _do_forward_solution('sample', fname_bti_raw, src=fname_src_small, bem=fname_bem_meg, mri=trans_path, eeg=False, meg=True, subjects_dir=subjects_dir)
```

### Step 10: Call _compare_forwards()

```python
_compare_forwards(fwd, fwd_py, 248, n_src_small)
```


## Complete Example

```python
# Setup
# Fixtures: fname_src_small

# Workflow
'Test BTI end-to-end versus C.'
bti_pdf = bti_dir / 'test_pdf_linux'
bti_config = bti_dir / 'test_config_linux'
bti_hs = bti_dir / 'test_hs_linux'
fname_bti_raw = bti_dir / 'exported4D_linux_raw.fif'
raw_py = read_raw_bti(bti_pdf, bti_config, bti_hs, preload=False)
src = read_source_spaces(fname_src_small)
fwd_py = make_forward_solution(raw_py.info, src=src, eeg=False, meg=True, bem=fname_bem_meg, trans=trans_path)
fwd = _do_forward_solution('sample', fname_bti_raw, src=fname_src_small, bem=fname_bem_meg, mri=trans_path, eeg=False, meg=True, subjects_dir=subjects_dir)
_compare_forwards(fwd, fwd_py, 248, n_src_small)
```

## Next Steps


---

*Source: test_make_forward.py:278 | Complexity: Advanced | Last updated: 2026-05-18*