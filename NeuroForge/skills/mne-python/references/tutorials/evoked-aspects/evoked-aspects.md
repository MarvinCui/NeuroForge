# How To: Evoked Aspects

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test handling of evoked aspects.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: aspect_kind, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test handling of evoked aspects.'

```python
'Test handling of evoked aspects.'
```

**Verification:**
```python
assert 'Evoked' in repr(ave)
```

### Step 2: Assign ave = read_evokeds(...)

```python
ave = read_evokeds(fname, 0)
```

**Verification:**
```python
assert_allclose(ave.data, ave_2.data)
```

### Step 3: Assign ave._aspect_kind = aspect_kind

```python
ave._aspect_kind = aspect_kind
```

**Verification:**
```python
assert ave.kind == ave_2.kind
```

### Step 4: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test-ave.fif'
```

### Step 5: Call ave.save()

```python
ave.save(temp_fname)
```

### Step 6: Assign ave_2 = read_evokeds(...)

```python
ave_2 = read_evokeds(temp_fname, condition=0)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(ave.data, ave_2.data)
```

**Verification:**
```python
assert ave.kind == ave_2.kind
```


## Complete Example

```python
# Setup
# Fixtures: aspect_kind, tmp_path

# Workflow
'Test handling of evoked aspects.'
ave = read_evokeds(fname, 0)
ave._aspect_kind = aspect_kind
assert 'Evoked' in repr(ave)
temp_fname = tmp_path / 'test-ave.fif'
ave.save(temp_fname)
ave_2 = read_evokeds(temp_fname, condition=0)
assert_allclose(ave.data, ave_2.data)
assert ave.kind == ave_2.kind
```

## Next Steps


---

*Source: test_evoked.py:191 | Complexity: Intermediate | Last updated: 2026-05-18*