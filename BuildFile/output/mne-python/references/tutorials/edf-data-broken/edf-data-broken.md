# How To: Edf Data Broken

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test edf files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test edf files.'

```python
'Test edf files.'
```

**Verification:**
```python
assert_equal(len(raw.ch_names) + 2, len(raw_py.ch_names))
```

### Step 2: Assign raw = _test_raw_reader(...)

```python
raw = _test_raw_reader(read_raw_edf, input_fname=edf_path, exclude=['Ergo-Left', 'H10'], verbose='error')
```

**Verification:**
```python
assert rbytes[184:192] == b'36096   '
```

### Step 3: Assign raw_py = read_raw_edf(...)

```python
raw_py = read_raw_edf(edf_path)
```

**Verification:**
```python
assert_allclose(data, data_new)
```

### Step 4: Assign data = raw_py.get_data(...)

```python
data = raw_py.get_data()
```

### Step 5: Call assert_equal()

```python
assert_equal(len(raw.ch_names) + 2, len(raw_py.ch_names))
```

### Step 6: Assign broken_fname = value

```python
broken_fname = tmp_path / 'broken.edf'
```

### Step 7: Assign raw_py = read_raw_edf(...)

```python
raw_py = read_raw_edf(broken_fname)
```

### Step 8: Assign data_new = raw_py.get_data(...)

```python
data_new = raw_py.get_data()
```

### Step 9: Call assert_allclose()

```python
assert_allclose(data, data_new)
```

### Step 10: Call fid_in.seek()

```python
fid_in.seek(0, 2)
```

### Step 11: Assign n_bytes = fid_in.tell(...)

```python
n_bytes = fid_in.tell()
```

### Step 12: Call fid_in.seek()

```python
fid_in.seek(0, 0)
```

### Step 13: Assign rbytes = fid_in.read(...)

```python
rbytes = fid_in.read()
```

### Step 14: Call fid_out.write()

```python
fid_out.write(rbytes[:236])
```

### Step 15: Call fid_out.write()

```python
fid_out.write(b'-1      ')
```

### Step 16: Call fid_out.write()

```python
fid_out.write(rbytes[244:244 + int(n_bytes * 0.4)])
```

### Step 17: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(broken_fname, preload=True)
```

### Step 18: Call read_raw_edf()

```python
read_raw_edf(broken_fname, exclude=raw.ch_names[:132], preload=True)
```

### Step 19: Call fid_out.write()

```python
fid_out.write(rbytes[:184])
```

**Verification:**
```python
assert rbytes[184:192] == b'36096   '
```

### Step 20: Call fid_out.write()

```python
fid_out.write(rbytes[184:192].replace(b' ', b'\x00'))
```

### Step 21: Call fid_out.write()

```python
fid_out.write(rbytes[192:])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test edf files.'
raw = _test_raw_reader(read_raw_edf, input_fname=edf_path, exclude=['Ergo-Left', 'H10'], verbose='error')
raw_py = read_raw_edf(edf_path)
data = raw_py.get_data()
assert_equal(len(raw.ch_names) + 2, len(raw_py.ch_names))
broken_fname = tmp_path / 'broken.edf'
with open(edf_path, 'rb') as fid_in:
    fid_in.seek(0, 2)
    n_bytes = fid_in.tell()
    fid_in.seek(0, 0)
    rbytes = fid_in.read()
with open(broken_fname, 'wb') as fid_out:
    fid_out.write(rbytes[:236])
    fid_out.write(b'-1      ')
    fid_out.write(rbytes[244:244 + int(n_bytes * 0.4)])
with pytest.warns(RuntimeWarning, match='records .* not match the file size'):
    raw = read_raw_edf(broken_fname, preload=True)
    read_raw_edf(broken_fname, exclude=raw.ch_names[:132], preload=True)
with open(broken_fname, 'wb') as fid_out:
    fid_out.write(rbytes[:184])
    assert rbytes[184:192] == b'36096   '
    fid_out.write(rbytes[184:192].replace(b' ', b'\x00'))
    fid_out.write(rbytes[192:])
raw_py = read_raw_edf(broken_fname)
data_new = raw_py.get_data()
assert_allclose(data, data_new)
```

## Next Steps


---

*Source: test_edf.py:281 | Complexity: Advanced | Last updated: 2026-05-18*