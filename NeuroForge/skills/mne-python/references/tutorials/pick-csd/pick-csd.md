# How To: Pick Csd

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking current source density channels.

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

### Step 1: 'Test picking current source density channels.'

```python
'Test picking current source density channels.'
```

**Verification:**
```python
assert_indexing(info, picks_by_type, all_data=False)
```

### Step 2: Assign names = value

```python
names = ['MEG 2331', 'MEG 2332', 'MEG 2333', 'A1', 'A2', 'Fz']
```

### Step 3: Assign types = unknown.split(...)

```python
types = 'mag mag grad csd csd csd'.split()
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(names, 1024.0, types)
```

### Step 5: Assign picks_by_type = value

```python
picks_by_type = [('mag', [0, 1]), ('grad', [2]), ('csd', [3, 4, 5])]
```

### Step 6: Call assert_indexing()

```python
assert_indexing(info, picks_by_type, all_data=False)
```


## Complete Example

```python
# Workflow
'Test picking current source density channels.'
names = ['MEG 2331', 'MEG 2332', 'MEG 2333', 'A1', 'A2', 'Fz']
types = 'mag mag grad csd csd csd'.split()
info = create_info(names, 1024.0, types)
picks_by_type = [('mag', [0, 1]), ('grad', [2]), ('csd', [3, 4, 5])]
assert_indexing(info, picks_by_type, all_data=False)
```

## Next Steps


---

*Source: test_pick.py:365 | Complexity: Intermediate | Last updated: 2026-05-18*