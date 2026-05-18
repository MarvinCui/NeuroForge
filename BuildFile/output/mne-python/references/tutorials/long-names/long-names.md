# How To: Long Names

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test long name support.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne.channels`
- `mne.io`
- `mne.io.array`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test long name support.'

```python
'Test long name support.'
```

**Verification:**
```python
assert raw.ch_names == ['a' * 15 + 'b', 'a' * 16]
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(['a' * 15 + 'b', 'a' * 16], 1000.0, verbose='error')
```

**Verification:**
```python
assert raw.ch_names == ['a' * 13 + '-0', 'a' * 13 + '-1']
```

### Step 3: Assign data = np.zeros(...)

```python
data = np.zeros((2, 1000))
```

**Verification:**
```python
assert raw.ch_names == ['a' * 16 + f'-{ii}' for ii in range(11)]
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

**Verification:**
```python
assert raw.ch_names == ['a' * 15 + 'b', 'a' * 16]
```

### Step 5: Call raw.rename_channels()

```python
raw.rename_channels({k: k[:13] for k in raw.ch_names}, allow_duplicates=True, verbose='error')
```

**Verification:**
```python
assert raw.ch_names == ['a' * 13 + '-0', 'a' * 13 + '-1']
```

### Step 6: Assign info = create_info(...)

```python
info = create_info(['a' * 16] * 11, 1000.0, verbose='error')
```

### Step 7: Assign data = np.zeros(...)

```python
data = np.zeros((11, 1000))
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

**Verification:**
```python
assert raw.ch_names == ['a' * 16 + f'-{ii}' for ii in range(11)]
```


## Complete Example

```python
# Workflow
'Test long name support.'
info = create_info(['a' * 15 + 'b', 'a' * 16], 1000.0, verbose='error')
data = np.zeros((2, 1000))
raw = RawArray(data, info)
assert raw.ch_names == ['a' * 15 + 'b', 'a' * 16]
raw.rename_channels({k: k[:13] for k in raw.ch_names}, allow_duplicates=True, verbose='error')
assert raw.ch_names == ['a' * 13 + '-0', 'a' * 13 + '-1']
info = create_info(['a' * 16] * 11, 1000.0, verbose='error')
data = np.zeros((11, 1000))
raw = RawArray(data, info)
assert raw.ch_names == ['a' * 16 + f'-{ii}' for ii in range(11)]
```

## Next Steps


---

*Source: test_array.py:24 | Complexity: Advanced | Last updated: 2026-05-18*