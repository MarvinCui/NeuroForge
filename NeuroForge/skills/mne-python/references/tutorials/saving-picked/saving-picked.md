# How To: Saving Picked

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test saving picked CTF instances.

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
# Fixtures: tmp_path, comp_grade
```

## Step-by-Step Guide

### Step 1: 'Test saving picked CTF instances.'

```python
'Test saving picked CTF instances.'
```

**Verification:**
```python
assert raw.info['meas_date'] == _stamp_to_dt((1367228160, 0))
```

### Step 2: Assign temp_dir = str(...)

```python
temp_dir = str(tmp_path)
```

**Verification:**
```python
assert raw.compensation_grade == get_current_comp(raw.info) == 0
```

### Step 3: Assign out_fname = op.join(...)

```python
out_fname = op.join(temp_dir, 'test_py_raw.fif')
```

**Verification:**
```python
assert len(raw.info['comps']) == 5
```

### Step 4: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(op.join(ctf_dir, ctf_fname_1_trial))
```

**Verification:**
```python
assert len(raw.info['comps']) == 5
```

### Step 5: Call raw.crop.load_data()

```python
raw.crop(0, 1).load_data()
```

**Verification:**
```python
assert len(raw_pick.info['comps']) == 0
```

### Step 6: Assign picks = _picks_to_idx(...)

```python
picks = _picks_to_idx(raw.info, 'meg', with_ref_meg=False)
```

**Verification:**
```python
assert 'Removing 5 compensators' in log
```

### Step 7: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(comp_grade)
```

**Verification:**
```python
assert raw_pick.ch_names == raw2.ch_names
```

### Step 8: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert_array_equal(raw_pick.times, raw2.times)
```

### Step 9: Call raw_pick.save()

```python
raw_pick.save(out_fname, overwrite=True)
```

**Verification:**
```python
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
```

### Step 10: Assign raw2 = read_raw_fif(...)

```python
raw2 = read_raw_fif(out_fname)
```

**Verification:**
```python
assert raw_pick.ch_names == raw2.ch_names
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(raw_pick.times, raw2.times)
```

**Verification:**
```python
assert_array_equal(raw_pick.times, raw2.times)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
```

**Verification:**
```python
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
```

### Step 13: Assign raw2 = read_raw_fif(...)

```python
raw2 = read_raw_fif(out_fname, preload=True)
```

**Verification:**
```python
assert raw_pick.ch_names == raw2.ch_names
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(raw_pick.times, raw2.times)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
```

### Step 16: Assign raw_pick = raw.copy.pick(...)

```python
raw_pick = raw.copy().pick(picks, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, comp_grade

# Workflow
'Test saving picked CTF instances.'
temp_dir = str(tmp_path)
out_fname = op.join(temp_dir, 'test_py_raw.fif')
raw = read_raw_ctf(op.join(ctf_dir, ctf_fname_1_trial))
assert raw.info['meas_date'] == _stamp_to_dt((1367228160, 0))
raw.crop(0, 1).load_data()
assert raw.compensation_grade == get_current_comp(raw.info) == 0
assert len(raw.info['comps']) == 5
picks = _picks_to_idx(raw.info, 'meg', with_ref_meg=False)
raw.apply_gradient_compensation(comp_grade)
with catch_logging() as log:
    raw_pick = raw.copy().pick(picks, verbose=True)
assert len(raw.info['comps']) == 5
assert len(raw_pick.info['comps']) == 0
log = log.getvalue()
assert 'Removing 5 compensators' in log
raw_pick.save(out_fname, overwrite=True)
raw2 = read_raw_fif(out_fname)
assert raw_pick.ch_names == raw2.ch_names
assert_array_equal(raw_pick.times, raw2.times)
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
raw2 = read_raw_fif(out_fname, preload=True)
assert raw_pick.ch_names == raw2.ch_names
assert_array_equal(raw_pick.times, raw2.times)
assert_allclose(raw2[0:20][0], raw_pick[0:20][0], rtol=1e-06, atol=1e-20)
```

## Next Steps


---

*Source: test_ctf.py:365 | Complexity: Advanced | Last updated: 2026-05-18*