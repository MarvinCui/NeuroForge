# How To: Open Report

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the open_report function.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `glob`
- `os`
- `pickle`
- `re`
- `shutil`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `matplotlib`
- `mne`
- `mne._fiff.write`
- `mne.datasets`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.report`
- `mne.report`
- `mne.report.report`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `sklearn.exceptions`
- `PIL`
- `pyvista.plotting.plotter`
- `pyvista.plotting.plotting`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test the open_report function.'

```python
'Test the open_report function.'
```

**Verification:**
```python
assert report.subjects_dir == str(tmp_path)
```

### Step 2: Assign h5py = pytest.importorskip(...)

```python
h5py = pytest.importorskip('h5py')
```

**Verification:**
```python
assert report.fname == str(hdf5)
```

### Step 3: Assign h5io = pytest.importorskip(...)

```python
h5io = pytest.importorskip('h5io')
```

**Verification:**
```python
assert Path(hdf5).exists()
```

### Step 4: Assign hdf5 = str(...)

```python
hdf5 = str(tmp_path / 'report.h5')
```

**Verification:**
```python
assert h5io.read_hdf5(hdf5, title='companion') == 'test'
```

### Step 5: Assign fig1 = value

```python
fig1 = _get_example_figures()[0]
```

**Verification:**
```python
assert report2.fname == str(hdf5)
```

### Step 6: Assign report2 = open_report(...)

```python
report2 = open_report(hdf5)
```

**Verification:**
```python
assert report2.subjects_dir == report.subjects_dir
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, open_report, hdf5, foo='bar')
```

**Verification:**
```python
assert report2.html == report.html
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, open_report, hdf5, subjects_dir='foo')
```

**Verification:**
```python
assert report2.__getstate__() == report.__getstate__()
```

### Step 9: Call open_report()

```python
open_report(hdf5, subjects_dir=str(tmp_path))
```

**Verification:**
```python
assert '_fname' not in report2.__getstate__()
```

### Step 10: Call report.add_figure()

```python
report.add_figure(fig=fig1, title='evoked response')
```

**Verification:**
```python
assert h5io.read_hdf5(hdf5, title='companion') == 'test'
```

### Step 11: Call h5io.write_hdf5()

```python
h5io.write_hdf5(f, 'test', title='companion')
```

**Verification:**
```python
assert h5io.read_hdf5(hdf5, title='companion') == 'test'
```

### Step 12: 1 / 0

```python
1 / 0
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test the open_report function.'
h5py = pytest.importorskip('h5py')
h5io = pytest.importorskip('h5io')
hdf5 = str(tmp_path / 'report.h5')
fig1 = _get_example_figures()[0]
with open_report(hdf5, subjects_dir=tmp_path) as report:
    assert report.subjects_dir == str(tmp_path)
    assert report.fname == str(hdf5)
    report.add_figure(fig=fig1, title='evoked response')
assert Path(hdf5).exists()
with h5py.File(hdf5, 'r+') as f:
    h5io.write_hdf5(f, 'test', title='companion')
assert h5io.read_hdf5(hdf5, title='companion') == 'test'
report2 = open_report(hdf5)
assert report2.fname == str(hdf5)
assert report2.subjects_dir == report.subjects_dir
assert report2.html == report.html
assert report2.__getstate__() == report.__getstate__()
assert '_fname' not in report2.__getstate__()
pytest.raises(ValueError, open_report, hdf5, foo='bar')
pytest.raises(ValueError, open_report, hdf5, subjects_dir='foo')
open_report(hdf5, subjects_dir=str(tmp_path))
with pytest.raises(ZeroDivisionError):
    with open_report(hdf5, subjects_dir=str(tmp_path)) as report:
        assert h5io.read_hdf5(hdf5, title='companion') == 'test'
        1 / 0
assert h5io.read_hdf5(hdf5, title='companion') == 'test'
```

## Next Steps


---

*Source: test_report.py:621 | Complexity: Advanced | Last updated: 2026-05-18*