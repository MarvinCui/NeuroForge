# How To: Pick Fnirs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking fNIRS channels.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test picking fNIRS channels.'

```python
'Test picking fNIRS channels.'
```

**Verification:**
```python
assert_indexing(info, picks_by_type)
```

### Step 2: Assign names = unknown.split(...)

```python
names = 'A1 A2 Fz O hbo1 hbo2 hbr1 fnirsRaw1 fnirsRaw2 fnirsOD1'.split()
```

### Step 3: Assign types = unknown.split(...)

```python
types = 'mag mag eeg eeg hbo hbo hbr fnirs_cw_amplitude fnirs_cw_amplitude fnirs_od'.split()
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(names, 1024.0, types)
```

### Step 5: Assign picks_by_type = value

```python
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('hbo', [4, 5]), ('hbr', [6]), ('fnirs_cw_amplitude', [7, 8]), ('fnirs_od', [9])]
```

### Step 6: Call assert_indexing()

```python
assert_indexing(info, picks_by_type)
```


## Complete Example

```python
# Workflow
'Test picking fNIRS channels.'
names = 'A1 A2 Fz O hbo1 hbo2 hbr1 fnirsRaw1 fnirsRaw2 fnirsOD1'.split()
types = 'mag mag eeg eeg hbo hbo hbr fnirs_cw_amplitude fnirs_cw_amplitude fnirs_od'.split()
info = create_info(names, 1024.0, types)
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('hbo', [4, 5]), ('hbr', [6]), ('fnirs_cw_amplitude', [7, 8]), ('fnirs_od', [9])]
assert_indexing(info, picks_by_type)
```

## Next Steps


---

*Source: test_pick.py:384 | Complexity: Intermediate | Last updated: 2026-05-18*