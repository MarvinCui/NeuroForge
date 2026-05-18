# How To: Setup Headshape

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading bti headshape.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `collections`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.bti.bti`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: hs
```

## Step-by-Step Guide

### Step 1: 'Test reading bti headshape.'

```python
'Test reading bti headshape.'
```

**Verification:**
```python
assert not expected - found
```

### Step 2: Assign unknown = _read_head_shape(...)

```python
nasion, lpa, rpa, hpi, dig_points = _read_head_shape(hs)
```

### Step 3: Assign unknown = _make_bti_dig_points(...)

```python
dig, t, _ = _make_bti_dig_points(nasion, lpa, rpa, hpi, dig_points)
```

### Step 4: Assign expected = value

```python
expected = {'kind', 'ident', 'r'}
```

### Step 5: Assign found = set(...)

```python
found = set(reduce(lambda x, y: list(x) + list(y), [d.keys() for d in dig]))
```

**Verification:**
```python
assert not expected - found
```


## Complete Example

```python
# Setup
# Fixtures: hs

# Workflow
'Test reading bti headshape.'
nasion, lpa, rpa, hpi, dig_points = _read_head_shape(hs)
dig, t, _ = _make_bti_dig_points(nasion, lpa, rpa, hpi, dig_points)
expected = {'kind', 'ident', 'r'}
found = set(reduce(lambda x, y: list(x) + list(y), [d.keys() for d in dig]))
assert not expected - found
```

## Next Steps


---

*Source: test_bti.py:377 | Complexity: Intermediate | Last updated: 2026-05-18*