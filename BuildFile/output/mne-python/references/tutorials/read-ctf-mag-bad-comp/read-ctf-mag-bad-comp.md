# How To: Read Ctf Mag Bad Comp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test CTF reader with mag comps and bad comps.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `os`
- `shutil`
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.io.ctf.info`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.io.ctf.constants`
- `mne.io.ctf.info`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test CTF reader with mag comps and bad comps.'

```python
'Test CTF reader with mag comps and bad comps.'
```

**Verification:**
```python
assert raw_orig.compensation_grade == 0
```

### Step 2: Assign path = op.join(...)

```python
path = op.join(ctf_dir, ctf_fname_continuous)
```

**Verification:**
```python
assert raw_mag_comp.compensation_grade == 0
```

### Step 3: Assign raw_orig = read_raw_ctf(...)

```python
raw_orig = read_raw_ctf(path)
```

**Verification:**
```python
assert src[0]['nuse'] == 26
```

### Step 4: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.io.ctf.ctf, '_read_res4', _read_res4_mag_comp)
```

**Verification:**
```python
assert_allclose(fwd_orig['sol']['data'], fwd_mag_comp['sol']['data'])
```

### Step 5: Assign raw_mag_comp = read_raw_ctf(...)

```python
raw_mag_comp = read_raw_ctf(path)
```

**Verification:**
```python
assert raw_mag_comp.compensation_grade == 0
```

### Step 6: Assign sphere = mne.make_sphere_model(...)

```python
sphere = mne.make_sphere_model()
```

### Step 7: Assign src = mne.setup_volume_source_space(...)

```python
src = mne.setup_volume_source_space(pos=50.0, exclude=5.0, bem=sphere)
```

**Verification:**
```python
assert src[0]['nuse'] == 26
```

### Step 8: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.io.ctf.ctf, '_read_res4', _bad_res4_grad_comp)
```

### Step 9: Call raw_orig.apply_gradient_compensation()

```python
raw_orig.apply_gradient_compensation(grade)
```

### Step 10: Call raw_mag_comp.apply_gradient_compensation()

```python
raw_mag_comp.apply_gradient_compensation(grade)
```

### Step 11: Assign args = value

```python
args = (None, src, sphere, True, False)
```

### Step 12: Assign fwd_orig = make_forward_solution(...)

```python
fwd_orig = make_forward_solution(raw_orig.info, *args)
```

### Step 13: Assign fwd_mag_comp = make_forward_solution(...)

```python
fwd_mag_comp = make_forward_solution(raw_mag_comp.info, *args)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(fwd_orig['sol']['data'], fwd_mag_comp['sol']['data'])
```

### Step 15: Call read_raw_ctf()

```python
read_raw_ctf(path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, monkeypatch

# Workflow
'Test CTF reader with mag comps and bad comps.'
path = op.join(ctf_dir, ctf_fname_continuous)
raw_orig = read_raw_ctf(path)
assert raw_orig.compensation_grade == 0
monkeypatch.setattr(mne.io.ctf.ctf, '_read_res4', _read_res4_mag_comp)
raw_mag_comp = read_raw_ctf(path)
assert raw_mag_comp.compensation_grade == 0
sphere = mne.make_sphere_model()
src = mne.setup_volume_source_space(pos=50.0, exclude=5.0, bem=sphere)
assert src[0]['nuse'] == 26
for grade in (0, 1):
    raw_orig.apply_gradient_compensation(grade)
    raw_mag_comp.apply_gradient_compensation(grade)
    args = (None, src, sphere, True, False)
    fwd_orig = make_forward_solution(raw_orig.info, *args)
    fwd_mag_comp = make_forward_solution(raw_mag_comp.info, *args)
    assert_allclose(fwd_orig['sol']['data'], fwd_mag_comp['sol']['data'])
monkeypatch.setattr(mne.io.ctf.ctf, '_read_res4', _bad_res4_grad_comp)
with pytest.raises(RuntimeError, match='inconsistent compensation grade'):
    read_raw_ctf(path)
```

## Next Steps


---

*Source: test_ctf.py:706 | Complexity: Advanced | Last updated: 2026-05-18*