# How To: Coodinates Extraction

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading of [Coordinates] section if present.

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

### Step 1: 'Test reading of [Coordinates] section if present.'

```python
'Test reading of [Coordinates] section if present.'
```

**Verification:**
```python
assert raw.info['dig'] is not None
```

### Step 2: Assign diglist = value

```python
diglist = raw.info['dig']
```

**Verification:**
```python
assert coords.shape == EXPECTED_SHAPE
```

### Step 3: Assign coords = np.array(...)

```python
coords = np.array([dig['r'] for dig in diglist])
```

**Verification:**
```python
assert coords.max() < 0.2
```

### Step 4: Assign EXPECTED_SHAPE = value

```python
EXPECTED_SHAPE = (len(raw.ch_names) - 4 + 3, 3)
```

**Verification:**
```python
assert raw2.info['dig'] is None
```

### Step 5: Assign raw2 = read_raw_brainvision(...)

```python
raw2 = read_raw_brainvision(vhdr_path)
```

**Verification:**
```python
assert raw2.info['dig'] is None
```

### Step 6: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(vhdr_v2_path)
```


## Complete Example

```python
# Workflow
'Test reading of [Coordinates] section if present.'
with _record_warnings(), pytest.warns(RuntimeWarning, match='coordinate information'):
    raw = read_raw_brainvision(vhdr_v2_path)
assert raw.info['dig'] is not None
diglist = raw.info['dig']
coords = np.array([dig['r'] for dig in diglist])
EXPECTED_SHAPE = (len(raw.ch_names) - 4 + 3, 3)
assert coords.shape == EXPECTED_SHAPE
assert coords.max() < 0.2
raw2 = read_raw_brainvision(vhdr_path)
assert raw2.info['dig'] is None
```

## Next Steps


---

*Source: test_brainvision.py:610 | Complexity: Intermediate | Last updated: 2026-05-18*