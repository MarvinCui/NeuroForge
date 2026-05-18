# How To: Concatenate Raws

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test error handling during raw concatenation.

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
# Fixtures: on_mismatch
```

## Step-by-Step Guide

### Step 1: 'Test error handling during raw concatenation.'

```python
'Test error handling during raw concatenation.'
```

### Step 2: Assign raw = read_raw_fif.crop(...)

```python
raw = read_raw_fif(fif_fname).crop(0, 10)
```

### Step 3: Assign raws = value

```python
raws = [raw, raw.copy()]
```

### Step 4: Assign kws = dict(...)

```python
kws = dict(raws=raws, on_mismatch=on_mismatch)
```

### Step 5: Call concatenate_raws()

```python
concatenate_raws(**kws)
```

### Step 6: Call concatenate_raws()

```python
concatenate_raws(**kws)
```

### Step 7: Call concatenate_raws()

```python
concatenate_raws(**kws)
```


## Complete Example

```python
# Setup
# Fixtures: on_mismatch

# Workflow
'Test error handling during raw concatenation.'
raw = read_raw_fif(fif_fname).crop(0, 10)
raws = [raw, raw.copy()]
raws[1].info['dev_head_t']['trans'] += 0.1
kws = dict(raws=raws, on_mismatch=on_mismatch)
if on_mismatch == 'ignore':
    concatenate_raws(**kws)
elif on_mismatch == 'warn':
    with pytest.warns(RuntimeWarning, match='different head positions'):
        concatenate_raws(**kws)
elif on_mismatch == 'raise':
    with pytest.raises(ValueError, match='different head positions'):
        concatenate_raws(**kws)
```

## Next Steps


---

*Source: test_raw_fiff.py:393 | Complexity: Intermediate | Last updated: 2026-05-18*