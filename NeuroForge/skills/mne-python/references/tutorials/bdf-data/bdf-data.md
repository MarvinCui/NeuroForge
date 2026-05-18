# How To: Bdf Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading raw bdf files.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test reading raw bdf files.'

```python
'Test reading raw bdf files.'
```

**Verification:**
```python
assert len(raw_py.ch_names) == 71
```

### Step 2: Assign test_scaling = False

```python
test_scaling = False
```

**Verification:**
```python
assert len(raw_py.ch_names) == 71
```

### Step 3: Assign raw_py = _test_raw_reader(...)

```python
raw_py = _test_raw_reader(read_raw_bdf, input_fname=bdf_path, eog=eog, misc=misc, exclude=['M2', 'IEOG'], test_scaling=test_scaling)
```

**Verification:**
```python
assert 'RawBDF' in repr(raw_py)
```

### Step 4: Assign raw_py = _test_raw_reader(...)

```python
raw_py = _test_raw_reader(read_raw_bdf, input_fname=bdf_path, montage='biosemi64', eog=eog, misc=misc, exclude=['M2', 'IEOG'], test_scaling=test_scaling)
```

**Verification:**
```python
assert_array_almost_equal(data_py, data_eeglab, 8)
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(raw_py.info, meg=False, eeg=True, exclude='bads')
```

**Verification:**
```python
assert raw_py.info['chs'][0]['loc'].any()
```

### Step 6: Assign unknown = value

```python
data_py, _ = raw_py[picks]
```

**Verification:**
```python
assert raw_py.info['chs'][25]['loc'].any()
```

### Step 7: Assign raw_eeglab = loadmat(...)

```python
raw_eeglab = loadmat(bdf_eeglab_path)
```

**Verification:**
```python
assert raw_py.info['chs'][63]['loc'].any()
```

### Step 8: Assign raw_eeglab = value

```python
raw_eeglab = raw_eeglab['data'] * 1e-06
```

### Step 9: Assign data_eeglab = value

```python
data_eeglab = raw_eeglab[picks]
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data_py, data_eeglab, 8)
```

**Verification:**
```python
assert raw_py.info['chs'][0]['loc'].any()
```


## Complete Example

```python
# Workflow
'Test reading raw bdf files.'
test_scaling = False
raw_py = _test_raw_reader(read_raw_bdf, input_fname=bdf_path, eog=eog, misc=misc, exclude=['M2', 'IEOG'], test_scaling=test_scaling)
assert len(raw_py.ch_names) == 71
raw_py = _test_raw_reader(read_raw_bdf, input_fname=bdf_path, montage='biosemi64', eog=eog, misc=misc, exclude=['M2', 'IEOG'], test_scaling=test_scaling)
assert len(raw_py.ch_names) == 71
assert 'RawBDF' in repr(raw_py)
picks = pick_types(raw_py.info, meg=False, eeg=True, exclude='bads')
data_py, _ = raw_py[picks]
raw_eeglab = loadmat(bdf_eeglab_path)
raw_eeglab = raw_eeglab['data'] * 1e-06
data_eeglab = raw_eeglab[picks]
assert_array_almost_equal(data_py, data_eeglab, 8)
assert raw_py.info['chs'][0]['loc'].any()
assert raw_py.info['chs'][25]['loc'].any()
assert raw_py.info['chs'][63]['loc'].any()
```

## Next Steps


---

*Source: test_edf.py:154 | Complexity: Advanced | Last updated: 2026-05-18*