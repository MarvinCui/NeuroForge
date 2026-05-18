# How To: Egi Mff Pause Chunks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that on-demand of all short segments works (via I/O).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.egi.egi`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that on-demand of all short segments works (via I/O).'

```python
'Test that on-demand of all short segments works (via I/O).'
```

**Verification:**
```python
assert_allclose(raw_data, raw_data_2)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

### Step 3: Assign fname_temp = value

```python
fname_temp = tmp_path / 'test_raw.fif'
```

### Step 4: Assign raw_data = read_raw_egi.get_data(...)

```python
raw_data = read_raw_egi(fname, preload=True).get_data()
```

### Step 5: Assign raw = read_raw_egi(...)

```python
raw = read_raw_egi(fname)
```

### Step 6: Assign raw_data_2 = read_raw_fif.get_data(...)

```python
raw_data_2 = read_raw_fif(fname_temp).get_data()
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw_data, raw_data_2)
```

### Step 8: Call raw.save()

```python
raw.save(fname_temp)
```


## Complete Example

```python
# Setup
# Fixtures: fname, tmp_path

# Workflow
'Test that on-demand of all short segments works (via I/O).'
pytest.importorskip('defusedxml')
fname_temp = tmp_path / 'test_raw.fif'
raw_data = read_raw_egi(fname, preload=True).get_data()
raw = read_raw_egi(fname)
with pytest.warns(RuntimeWarning, match='Acquisition skips detected'):
    raw.save(fname_temp)
del raw
raw_data_2 = read_raw_fif(fname_temp).get_data()
assert_allclose(raw_data, raw_data_2)
```

## Next Steps


---

*Source: test_egi.py:131 | Complexity: Advanced | Last updated: 2026-05-18*