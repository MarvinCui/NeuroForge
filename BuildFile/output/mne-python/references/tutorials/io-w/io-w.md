# How To: Io W

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test IO for w files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `re`
- `contextlib`
- `copy`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy`
- `scipy.optimize`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.morph_map`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test IO for w files.'

```python
'Test IO for w files.'
```

**Verification:**
```python
assert_array_almost_equal(src.data, src2.data)
```

### Step 2: Assign stc = _fake_stc(...)

```python
stc = _fake_stc(n_time=1)
```

**Verification:**
```python
assert_array_almost_equal(src.lh_vertno, src2.lh_vertno)
```

### Step 3: Assign w_fname = value

```python
w_fname = tmp_path / 'fake'
```

**Verification:**
```python
assert_array_almost_equal(src.rh_vertno, src2.rh_vertno)
```

### Step 4: Call stc.save()

```python
stc.save(w_fname, ftype='w')
```

### Step 5: Assign src = read_source_estimate(...)

```python
src = read_source_estimate(w_fname)
```

### Step 6: Call src.save()

```python
src.save(tmp_path / 'tmp', ftype='w')
```

### Step 7: Assign src2 = read_source_estimate(...)

```python
src2 = read_source_estimate(tmp_path / 'tmp-lh.w')
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(src.data, src2.data)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(src.lh_vertno, src2.lh_vertno)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(src.rh_vertno, src2.rh_vertno)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test IO for w files.'
stc = _fake_stc(n_time=1)
w_fname = tmp_path / 'fake'
stc.save(w_fname, ftype='w')
src = read_source_estimate(w_fname)
src.save(tmp_path / 'tmp', ftype='w')
src2 = read_source_estimate(tmp_path / 'tmp-lh.w')
assert_array_almost_equal(src.data, src2.data)
assert_array_almost_equal(src.lh_vertno, src2.lh_vertno)
assert_array_almost_equal(src.rh_vertno, src2.rh_vertno)
```

## Next Steps


---

*Source: test_source_estimate.py:531 | Complexity: Advanced | Last updated: 2026-05-18*