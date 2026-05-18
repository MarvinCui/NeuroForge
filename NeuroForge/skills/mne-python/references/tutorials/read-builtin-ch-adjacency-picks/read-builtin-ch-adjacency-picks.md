# How To: Read Builtin Ch Adjacency Picks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test picking channel subsets when reading builtin adjacency matrices.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: name, picks
```

## Step-by-Step Guide

### Step 1: 'Test picking channel subsets when reading builtin adjacency matrices.'

```python
'Test picking channel subsets when reading builtin adjacency matrices.'
```

**Verification:**
```python
assert_equal(ch_adjacency.shape[0], len(ch_names))
```

### Step 2: Assign unknown = read_ch_adjacency(...)

```python
ch_adjacency, ch_names = read_ch_adjacency(name)
```

**Verification:**
```python
assert picks == 'pick-names'
```

### Step 3: Call assert_equal()

```python
assert_equal(ch_adjacency.shape[0], len(ch_names))
```

**Verification:**
```python
assert_array_equal(ch_subset_names, subset_names)
```

### Step 4: Assign subset_names = value

```python
subset_names = ch_names[::2]
```

### Step 5: Assign unknown = read_ch_adjacency(...)

```python
ch_subset_adjacency, ch_subset_names = read_ch_adjacency(name, subset)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(ch_subset_names, subset_names)
```

### Step 7: Assign subset = slice(...)

```python
subset = slice(None, None, 2)
```

### Step 8: Assign subset = np.arange(...)

```python
subset = np.arange(0, len(ch_names), 2)
```

**Verification:**
```python
assert picks == 'pick-names'
```

### Step 9: Assign subset = subset_names

```python
subset = subset_names
```


## Complete Example

```python
# Setup
# Fixtures: name, picks

# Workflow
'Test picking channel subsets when reading builtin adjacency matrices.'
ch_adjacency, ch_names = read_ch_adjacency(name)
assert_equal(ch_adjacency.shape[0], len(ch_names))
subset_names = ch_names[::2]
if picks == 'pick-slice':
    subset = slice(None, None, 2)
elif picks == 'pick-arange':
    subset = np.arange(0, len(ch_names), 2)
else:
    assert picks == 'pick-names'
    subset = subset_names
ch_subset_adjacency, ch_subset_names = read_ch_adjacency(name, subset)
assert_array_equal(ch_subset_names, subset_names)
```

## Next Steps


---

*Source: test_channels.py:252 | Complexity: Advanced | Last updated: 2026-05-18*