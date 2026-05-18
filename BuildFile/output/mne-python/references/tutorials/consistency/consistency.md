# How To: Consistency

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test defaults consistency.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pytest`
- `numpy.testing`
- `mne.defaults`
- `mne.io.base`

**Setup Required:**
```python
# Fixtures: key
```

## Step-by-Step Guide

### Step 1: 'Test defaults consistency.'

```python
'Test defaults consistency.'
```

**Verification:**
```python
assert au_keys.intersection(units) == set()
```

### Step 2: Assign units = set(...)

```python
units = set(_handle_default('units'))
```

**Verification:**
```python
assert au_keys.issubset(other)
```

### Step 3: Assign other = set(...)

```python
other = set(_handle_default(key))
```

**Verification:**
```python
assert au_keys.intersection(other) == set()
```

### Step 4: Assign au_keys = set(...)

```python
au_keys = set('stim exci syst resp ias chpi'.split())
```

**Verification:**
```python
assert units == other, key
```

### Step 5: Assign other = other.difference(...)

```python
other = other.difference(au_keys)
```

**Verification:**
```python
assert au_keys.intersection(other) == set()
```


## Complete Example

```python
# Setup
# Fixtures: key

# Workflow
'Test defaults consistency.'
units = set(_handle_default('units'))
other = set(_handle_default(key))
au_keys = set('stim exci syst resp ias chpi'.split())
assert au_keys.intersection(units) == set()
if key in ('color', 'scalings_plot_raw'):
    assert au_keys.issubset(other)
    other = other.difference(au_keys)
else:
    assert au_keys.intersection(other) == set()
assert units == other, key
```

## Next Steps


---

*Source: test_defaults.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*