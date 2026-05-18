# How To: Show Fiff

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test show_fiff.

## Prerequisites

**Required Modules:**
- `pathlib`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test show_fiff.'

```python
'Test show_fiff.'
```

**Verification:**
```python
assert 'BAD' not in info
```

### Step 2: Assign info = show_fiff(...)

```python
info = show_fiff(fname_evoked)
```

**Verification:**
```python
assert all((key in info for key in keys))
```

### Step 3: Assign keys = value

```python
keys = ['FIFF_EPOCH', 'FIFFB_HPI_COIL', 'FIFFB_PROJ_ITEM', 'FIFFB_PROCESSED_DATA', 'FIFFB_EVOKED', 'FIFF_NAVE', 'FIFF_EPOCH', 'COORD_TRANS']
```

**Verification:**
```python
assert 'BAD' not in info
```

### Step 4: Assign info = show_fiff(...)

```python
info = show_fiff(fname_raw, read_limit=1024)
```

**Verification:**
```python
assert 'BAD' not in info
```

### Step 5: Assign info = show_fiff(...)

```python
info = show_fiff(fname_c_annot)
```

**Verification:**
```python
assert '>B' in info, info
```


## Complete Example

```python
# Workflow
'Test show_fiff.'
info = show_fiff(fname_evoked)
assert 'BAD' not in info
keys = ['FIFF_EPOCH', 'FIFFB_HPI_COIL', 'FIFFB_PROJ_ITEM', 'FIFFB_PROCESSED_DATA', 'FIFFB_EVOKED', 'FIFF_NAVE', 'FIFF_EPOCH', 'COORD_TRANS']
assert all((key in info for key in keys))
info = show_fiff(fname_raw, read_limit=1024)
assert 'BAD' not in info
info = show_fiff(fname_c_annot)
assert 'BAD' not in info
assert '>B' in info, info
```

## Next Steps


---

*Source: test_show_fiff.py:15 | Complexity: Intermediate | Last updated: 2026-05-18*