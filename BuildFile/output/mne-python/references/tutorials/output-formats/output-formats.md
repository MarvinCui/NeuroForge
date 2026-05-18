# How To: Output Formats

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test saving and loading raw data using multiple formats.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `os`
- `pathlib`
- `pickle`
- `platform`
- `shutil`
- `contextlib`
- `copy`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test saving and loading raw data using multiple formats.'

```python
'Test saving and loading raw data using multiple formats.'
```

**Verification:**
```python
assert_allclose(raw2_data, raw[:, :][0], rtol=tol, atol=1e-25)
```

### Step 2: Assign formats = value

```python
formats = ['short', 'int', 'single', 'double']
```

**Verification:**
```python
assert raw2.orig_format == fmt
```

### Step 3: Assign tols = value

```python
tols = [0.0001, 1e-07, 1e-07, 1e-15]
```

### Step 4: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(test_fif_fname).crop(0, 1)
```

### Step 5: Assign temp_file = value

```python
temp_file = tmp_path / 'raw.fif'
```

### Step 6: Call raw.save()

```python
raw.save(temp_file, fmt=fmt, overwrite=True)
```

### Step 7: Assign raw2 = read_raw_fif(...)

```python
raw2 = read_raw_fif(temp_file)
```

### Step 8: Assign raw2_data = value

```python
raw2_data = raw2[:, :][0]
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw2_data, raw[:, :][0], rtol=tol, atol=1e-25)
```

**Verification:**
```python
assert raw2.orig_format == fmt
```

### Step 10: Call pytest.raises()

```python
pytest.raises(OSError, raw.save, temp_file, fmt=fmt)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test saving and loading raw data using multiple formats.'
formats = ['short', 'int', 'single', 'double']
tols = [0.0001, 1e-07, 1e-07, 1e-15]
raw = read_raw_fif(test_fif_fname).crop(0, 1)
temp_file = tmp_path / 'raw.fif'
for ii, (fmt, tol) in enumerate(zip(formats, tols)):
    if ii > 0:
        pytest.raises(OSError, raw.save, temp_file, fmt=fmt)
    raw.save(temp_file, fmt=fmt, overwrite=True)
    raw2 = read_raw_fif(temp_file)
    raw2_data = raw2[:, :][0]
    assert_allclose(raw2_data, raw[:, :][0], rtol=tol, atol=1e-25)
    assert raw2.orig_format == fmt
```

## Next Steps


---

*Source: test_raw_fiff.py:225 | Complexity: Advanced | Last updated: 2026-05-18*