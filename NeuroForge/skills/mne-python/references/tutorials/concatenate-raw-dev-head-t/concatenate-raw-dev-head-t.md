# How To: Concatenate Raw Dev Head T

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test concatenating raws with dev-head-t including nans.

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

### Step 1: 'Test concatenating raws with dev-head-t including nans.'

```python
'Test concatenating raws with dev-head-t including nans.'
```

### Step 2: Assign data = np.random.randn(...)

```python
data = np.random.randn(3, 10)
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(3, 1000.0, ['mag', 'grad', 'grad'])
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 5: Assign unknown = Transform(...)

```python
raw.info['dev_head_t'] = Transform('meg', 'head', np.eye(4))
```

### Step 6: Assign unknown = value

```python
raw.info['dev_head_t']['trans'][0, 0] = np.nan
```

### Step 7: Assign raw2 = raw.copy(...)

```python
raw2 = raw.copy()
```

### Step 8: Call concatenate_raws()

```python
concatenate_raws([raw, raw2])
```


## Complete Example

```python
# Workflow
'Test concatenating raws with dev-head-t including nans.'
data = np.random.randn(3, 10)
info = create_info(3, 1000.0, ['mag', 'grad', 'grad'])
raw = RawArray(data, info)
raw.info['dev_head_t'] = Transform('meg', 'head', np.eye(4))
raw.info['dev_head_t']['trans'][0, 0] = np.nan
raw2 = raw.copy()
concatenate_raws([raw, raw2])
```

## Next Steps


---

*Source: test_raw.py:1069 | Complexity: Advanced | Last updated: 2026-05-18*