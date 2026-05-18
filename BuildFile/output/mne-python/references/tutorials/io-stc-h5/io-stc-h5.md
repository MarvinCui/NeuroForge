# How To: Io Stc H5

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test IO for STC files using HDF5.

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
# Fixtures: tmp_path, is_complex, vector
```

## Step-by-Step Guide

### Step 1: 'Test IO for STC files using HDF5.'

```python
'Test IO for STC files using HDF5.'
```

**Verification:**
```python
assert out_name.with_name(out_name.name + '-stc.h5').is_file()
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('h5io')
```

**Verification:**
```python
assert_equal(stc_new.subject, stc.subject)
```

### Step 3: Assign match = value

```python
match = 'can only be written' if vector else "Invalid value for the 'ftype"
```

**Verification:**
```python
assert_array_equal(stc_new.data, stc.data)
```

### Step 4: Assign out_name = value

```python
out_name = tmp_path / 'tmp'
```

**Verification:**
```python
assert_array_equal(stc_new.tmin, stc.tmin)
```

### Step 5: Call stc.save()

```python
stc.save(out_name, ftype='h5')
```

**Verification:**
```python
assert_array_equal(stc_new.tstep, stc.tstep)
```

### Step 6: Call stc.save()

```python
stc.save(out_name, ftype='h5', overwrite=True)
```

**Verification:**
```python
assert_equal(len(stc_new.vertices), len(stc.vertices))
```

### Step 7: Assign stc3 = read_source_estimate(...)

```python
stc3 = read_source_estimate(out_name)
```

**Verification:**
```python
assert_array_equal(v1, v2)
```

### Step 8: Assign stc4 = read_source_estimate(...)

```python
stc4 = read_source_estimate(out_name.with_name(out_name.name + '-stc'))
```

### Step 9: Assign stc5 = read_source_estimate(...)

```python
stc5 = read_source_estimate(out_name.with_name(out_name.name + '-stc.h5'))
```

### Step 10: Call pytest.raises()

```python
pytest.raises(RuntimeError, read_source_estimate, out_name, subject='bar')
```

### Step 11: Assign stc = _fake_vec_stc(...)

```python
stc = _fake_vec_stc(is_complex=is_complex)
```

### Step 12: Assign stc = _fake_stc(...)

```python
stc = _fake_stc(is_complex=is_complex)
```

### Step 13: Call stc.save()

```python
stc.save(tmp_path / 'tmp.h5', ftype='foo')
```

### Step 14: Call stc.save()

```python
stc.save(out_name, ftype='h5')
```

### Step 15: Call assert_equal()

```python
assert_equal(stc_new.subject, stc.subject)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(stc_new.data, stc.data)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(stc_new.tmin, stc.tmin)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(stc_new.tstep, stc.tstep)
```

### Step 19: Call assert_equal()

```python
assert_equal(len(stc_new.vertices), len(stc.vertices))
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(v1, v2)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, is_complex, vector

# Workflow
'Test IO for STC files using HDF5.'
pytest.importorskip('h5io')
if vector:
    stc = _fake_vec_stc(is_complex=is_complex)
else:
    stc = _fake_stc(is_complex=is_complex)
match = 'can only be written' if vector else "Invalid value for the 'ftype"
with pytest.raises(ValueError, match=match):
    stc.save(tmp_path / 'tmp.h5', ftype='foo')
out_name = tmp_path / 'tmp'
stc.save(out_name, ftype='h5')
assert out_name.with_name(out_name.name + '-stc.h5').is_file()
with pytest.raises(FileExistsError, match='Destination file exists'):
    stc.save(out_name, ftype='h5')
stc.save(out_name, ftype='h5', overwrite=True)
stc3 = read_source_estimate(out_name)
stc4 = read_source_estimate(out_name.with_name(out_name.name + '-stc'))
stc5 = read_source_estimate(out_name.with_name(out_name.name + '-stc.h5'))
pytest.raises(RuntimeError, read_source_estimate, out_name, subject='bar')
for stc_new in (stc3, stc4, stc5):
    assert_equal(stc_new.subject, stc.subject)
    assert_array_equal(stc_new.data, stc.data)
    assert_array_equal(stc_new.tmin, stc.tmin)
    assert_array_equal(stc_new.tstep, stc.tstep)
    assert_equal(len(stc_new.vertices), len(stc.vertices))
    for v1, v2 in zip(stc_new.vertices, stc.vertices):
        assert_array_equal(v1, v2)
```

## Next Steps


---

*Source: test_source_estimate.py:500 | Complexity: Advanced | Last updated: 2026-05-18*