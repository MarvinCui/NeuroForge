# How To: Channel Order

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that logical channel order is preserved.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, want_order
```

## Step-by-Step Guide

### Step 1: 'Test that logical channel order is preserved.'

```python
'Test that logical channel order is preserved.'
```

**Verification:**
```python
assert prefixes[::2] == prefixes[1::2]
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname)
```

**Verification:**
```python
assert prefixes == want_order
```

### Step 3: Assign ch_names = value

```python
ch_names = raw.ch_names
```

### Step 4: Assign prefixes = value

```python
prefixes = [ch_name.split()[0] for ch_name in ch_names]
```

**Verification:**
```python
assert prefixes[::2] == prefixes[1::2]
```

### Step 5: Assign prefixes = value

```python
prefixes = prefixes[::2]
```

**Verification:**
```python
assert prefixes == want_order
```


## Complete Example

```python
# Setup
# Fixtures: fname, want_order

# Workflow
'Test that logical channel order is preserved.'
raw = read_raw_nirx(fname)
ch_names = raw.ch_names
prefixes = [ch_name.split()[0] for ch_name in ch_names]
assert prefixes[::2] == prefixes[1::2]
prefixes = prefixes[::2]
assert prefixes == want_order
```

## Next Steps


---

*Source: test_nirx.py:803 | Complexity: Intermediate | Last updated: 2026-05-18*