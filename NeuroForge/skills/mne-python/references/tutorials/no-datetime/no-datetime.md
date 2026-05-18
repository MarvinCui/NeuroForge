# How To: No Datetime

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading a file with no datetime.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.eyelink._utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading a file with no datetime.'

```python
'Test reading a file with no datetime.'
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 2: Assign out_file = value

```python
out_file = tmp_path / 'tmp_eyelink.asc'
```

### Step 3: Assign unknown = value

```python
lines[1] = lines[1].split(':')[0] + ':'
```

### Step 4: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(out_file)
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(raw.annotations.onset[0], 0.004)
```

### Step 6: Assign lines = file.readlines(...)

```python
lines = file.readlines()
```

### Step 7: Call file.writelines()

```python
file.writelines(lines)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading a file with no datetime.'
out_file = tmp_path / 'tmp_eyelink.asc'
with open(fname) as file:
    lines = file.readlines()
lines[1] = lines[1].split(':')[0] + ':'
with open(out_file, 'w') as file:
    file.writelines(lines)
raw = read_raw_eyelink(out_file)
assert raw.info['meas_date'] is None
np.testing.assert_allclose(raw.annotations.onset[0], 0.004)
```

## Next Steps


---

*Source: test_eyelink.py:486 | Complexity: Intermediate | Last updated: 2026-05-18*