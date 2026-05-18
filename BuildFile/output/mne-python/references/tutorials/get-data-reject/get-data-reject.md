# How To: Get Data Reject

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if reject_by_annotation is working correctly.

## Prerequisites

**Required Modules:**
- `math`
- `os`
- `re`
- `contextlib`
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne._fiff.utils`
- `mne.io`
- `mne.io.base`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test if reject_by_annotation is working correctly.'

```python
'Test if reject_by_annotation is working correctly.'
```

**Verification:**
```python
assert log.getvalue().strip() == msg
```

### Step 2: Assign fs = 256

```python
fs = 256
```

**Verification:**
```python
assert data.shape == (len(ch_names), 1536)
```

### Step 3: Assign ch_names = value

```python
ch_names = ['C3', 'Cz', 'C4']
```

**Verification:**
```python
assert log.getvalue().strip() == msg
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=fs)
```

**Verification:**
```python
assert data.shape == (len(ch_names), 2560)
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((len(ch_names), 10 * fs)), info)
```

**Verification:**
```python
assert np.isnan(data).sum() == 3072
```

### Step 6: Call raw.set_annotations()

```python
raw.set_annotations(Annotations(onset=[2, 4], duration=[3, 2], description='bad'))
```

**Verification:**
```python
assert data.shape == (len(ch_names), 1536)
```

### Step 7: Assign data = raw.get_data(...)

```python
data = raw.get_data(reject_by_annotation='omit', verbose=True)
```

### Step 8: Assign msg = value

```python
msg = 'Omitting 1024 of 2560 (40.00%) samples, retaining 1536' + ' (60.00%) samples.'
```

**Verification:**
```python
assert log.getvalue().strip() == msg
```

### Step 9: Assign data = raw.get_data(...)

```python
data = raw.get_data(reject_by_annotation='nan', verbose=True)
```

### Step 10: Assign msg = value

```python
msg = 'Setting 1024 of 2560 (40.00%) samples to NaN, retaining 1536' + ' (60.00%) samples.'
```

**Verification:**
```python
assert log.getvalue().strip() == msg
```


## Complete Example

```python
# Workflow
'Test if reject_by_annotation is working correctly.'
fs = 256
ch_names = ['C3', 'Cz', 'C4']
info = create_info(ch_names, sfreq=fs)
raw = RawArray(np.zeros((len(ch_names), 10 * fs)), info)
raw.set_annotations(Annotations(onset=[2, 4], duration=[3, 2], description='bad'))
with catch_logging() as log:
    data = raw.get_data(reject_by_annotation='omit', verbose=True)
    msg = 'Omitting 1024 of 2560 (40.00%) samples, retaining 1536' + ' (60.00%) samples.'
    assert log.getvalue().strip() == msg
assert data.shape == (len(ch_names), 1536)
with catch_logging() as log:
    data = raw.get_data(reject_by_annotation='nan', verbose=True)
    msg = 'Setting 1024 of 2560 (40.00%) samples to NaN, retaining 1536' + ' (60.00%) samples.'
    assert log.getvalue().strip() == msg
assert data.shape == (len(ch_names), 2560)
assert np.isnan(data).sum() == 3072
```

## Next Steps


---

*Source: test_raw.py:715 | Complexity: Advanced | Last updated: 2026-05-18*