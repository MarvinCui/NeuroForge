# How To: Spectrum Proj

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that proj is applied correctly (gh 11177).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: inst, request
```

## Step-by-Step Guide

### Step 1: 'Test that proj is applied correctly (gh 11177).'

```python
'Test that proj is applied correctly (gh 11177).'
```

**Verification:**
```python
assert not np.array_equal(has_proj.get_data(), no_proj.get_data())
```

### Step 2: Assign inst = request.getfixturevalue(...)

```python
inst = request.getfixturevalue(inst)
```

**Verification:**
```python
assert has_proj == no_proj
```

### Step 3: Assign has_proj = inst.compute_psd(...)

```python
has_proj = inst.compute_psd(proj=True)
```

### Step 4: Assign no_proj = inst.compute_psd(...)

```python
no_proj = inst.compute_psd(proj=False)
```

**Verification:**
```python
assert not np.array_equal(has_proj.get_data(), no_proj.get_data())
```

### Step 5: Assign has_proj._data = value

```python
has_proj._data = no_proj._data
```

**Verification:**
```python
assert has_proj == no_proj
```

### Step 6: Assign unknown = value

```python
has_proj.info['projs'] = no_proj.info['projs']
```


## Complete Example

```python
# Setup
# Fixtures: inst, request

# Workflow
'Test that proj is applied correctly (gh 11177).'
inst = request.getfixturevalue(inst)
has_proj = inst.compute_psd(proj=True)
no_proj = inst.compute_psd(proj=False)
assert not np.array_equal(has_proj.get_data(), no_proj.get_data())
has_proj._data = no_proj._data
with has_proj.info._unlock():
    has_proj.info['projs'] = no_proj.info['projs']
assert has_proj == no_proj
```

## Next Steps


---

*Source: test_spectrum.py:466 | Complexity: Intermediate | Last updated: 2026-05-18*