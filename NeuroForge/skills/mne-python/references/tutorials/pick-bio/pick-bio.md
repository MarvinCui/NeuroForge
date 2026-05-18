# How To: Pick Bio

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking BIO channels.

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

### Step 1: 'Test picking BIO channels.'

```python
'Test picking BIO channels.'
```

**Verification:**
```python
assert_indexing(info, picks_by_type, all_data=False)
```

### Step 2: Assign names = unknown.split(...)

```python
names = 'A1 A2 Fz O BIO1 BIO2 BIO3'.split()
```

### Step 3: Assign types = unknown.split(...)

```python
types = 'mag mag eeg eeg bio bio bio'.split()
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(names, 1024.0, types)
```

### Step 5: Assign picks_by_type = value

```python
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('bio', [4, 5, 6])]
```

### Step 6: Call assert_indexing()

```python
assert_indexing(info, picks_by_type, all_data=False)
```


## Complete Example

```python
# Workflow
'Test picking BIO channels.'
names = 'A1 A2 Fz O BIO1 BIO2 BIO3'.split()
types = 'mag mag eeg eeg bio bio bio'.split()
info = create_info(names, 1024.0, types)
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('bio', [4, 5, 6])]
assert_indexing(info, picks_by_type, all_data=False)
```

## Next Steps


---

*Source: test_pick.py:375 | Complexity: Intermediate | Last updated: 2026-05-18*