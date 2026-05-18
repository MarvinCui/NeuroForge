# How To: Ignore Marker Types

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ignore marker types.

## Prerequisites

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test ignore marker types.'

```python
'Test ignore marker types.'
```

**Verification:**
```python
assert_array_equal(raw.annotations.description, expected_descriptions)
```

### Step 2: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(vhdr_path)
```

**Verification:**
```python
assert_array_equal(raw.annotations.description, expected_descriptions)
```

### Step 3: Assign expected_descriptions = value

```python
expected_descriptions = ['Stimulus/S253', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Stimulus/S253', 'Stimulus/S255', 'Response/R255', 'Event/254', 'Stimulus/S255', 'SyncStatus/Sync On', 'Optic/O  1']
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description, expected_descriptions)
```

### Step 5: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(vhdr_path, ignore_marker_types=True)
```

### Step 6: Assign expected_descriptions = value

```python
expected_descriptions = ['S253', 'S255', '254', 'S255', '254', 'S255', 'S253', 'S255', 'R255', '254', 'S255', 'Sync On', 'O  1']
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description, expected_descriptions)
```


## Complete Example

```python
# Workflow
'Test ignore marker types.'
raw = read_raw_brainvision(vhdr_path)
expected_descriptions = ['Stimulus/S253', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Event/254', 'Stimulus/S255', 'Stimulus/S253', 'Stimulus/S255', 'Response/R255', 'Event/254', 'Stimulus/S255', 'SyncStatus/Sync On', 'Optic/O  1']
assert_array_equal(raw.annotations.description, expected_descriptions)
raw = read_raw_brainvision(vhdr_path, ignore_marker_types=True)
expected_descriptions = ['S253', 'S255', '254', 'S255', '254', 'S255', 'S253', 'S255', 'R255', '254', 'S255', 'Sync On', 'O  1']
assert_array_equal(raw.annotations.description, expected_descriptions)
```

## Next Steps


---

*Source: test_brainvision.py:665 | Complexity: Intermediate | Last updated: 2026-05-18*