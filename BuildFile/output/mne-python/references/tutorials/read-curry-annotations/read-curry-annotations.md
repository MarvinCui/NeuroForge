# How To: Read Curry Annotations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading for Curry events file.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io.bti`
- `mne.io.curry`
- `mne.io.curry.curry`
- `mne.io.edf`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test reading for Curry events file.'

```python
'Test reading for Curry events file.'
```

**Verification:**
```python
assert annot.orig_time is None
```

### Step 2: Assign EXPECTED_ONSET = value

```python
EXPECTED_ONSET = [0.484, 0.486, 0.62, 0.622, 1.904, 1.906, 3.212, 3.214, 4.498, 4.5, 5.8, 5.802, 7.074, 7.076, 8.324, 8.326, 9.58, 9.582]
```

**Verification:**
```python
assert_array_equal(annot.onset, EXPECTED_ONSET)
```

### Step 3: Assign EXPECTED_DURATION = np.zeros_like(...)

```python
EXPECTED_DURATION = np.zeros_like(EXPECTED_ONSET)
```

**Verification:**
```python
assert_array_equal(annot.duration, EXPECTED_DURATION)
```

### Step 4: Assign EXPECTED_DESCRIPTION = value

```python
EXPECTED_DESCRIPTION = ['4', '50000', '2', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000']
```

**Verification:**
```python
assert_array_equal(annot.description, EXPECTED_DESCRIPTION)
```

### Step 5: Assign annot = read_annotations(...)

```python
annot = read_annotations(fname, sfreq='auto')
```

**Verification:**
```python
assert annot.orig_time is None
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(annot.onset, EXPECTED_ONSET)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(annot.duration, EXPECTED_DURATION)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(annot.description, EXPECTED_DESCRIPTION)
```

### Step 9: Assign _ = read_annotations(...)

```python
_ = read_annotations(fname, sfreq='nonsense')
```

### Step 10: Assign _ = read_annotations(...)

```python
_ = read_annotations(fname, sfreq=12.0)
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test reading for Curry events file.'
EXPECTED_ONSET = [0.484, 0.486, 0.62, 0.622, 1.904, 1.906, 3.212, 3.214, 4.498, 4.5, 5.8, 5.802, 7.074, 7.076, 8.324, 8.326, 9.58, 9.582]
EXPECTED_DURATION = np.zeros_like(EXPECTED_ONSET)
EXPECTED_DESCRIPTION = ['4', '50000', '2', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000', '1', '50000']
annot = read_annotations(fname, sfreq='auto')
assert annot.orig_time is None
assert_array_equal(annot.onset, EXPECTED_ONSET)
assert_array_equal(annot.duration, EXPECTED_DURATION)
assert_array_equal(annot.description, EXPECTED_DESCRIPTION)
with pytest.raises(ValueError, match="must be numeric or 'auto'"):
    _ = read_annotations(fname, sfreq='nonsense')
with pytest.warns(RuntimeWarning, match='does not match freq from fileheader'):
    _ = read_annotations(fname, sfreq=12.0)
```

## Next Steps


---

*Source: test_curry.py:464 | Complexity: Advanced | Last updated: 2026-05-18*