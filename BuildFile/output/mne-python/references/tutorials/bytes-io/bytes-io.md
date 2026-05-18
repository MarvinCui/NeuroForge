# How To: Bytes Io

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test bti bytes-io API.

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
# Fixtures: pdf, config, hs, exported
```

## Step-by-Step Guide

### Step 1: 'Test bti bytes-io API.'

```python
'Test bti bytes-io API.'
```

**Verification:**
```python
assert_array_equal(raw[:][0], raw2[:][0])
```

### Step 2: Assign raw = read_raw_bti(...)

```python
raw = read_raw_bti(pdf, config, hs, convert=True, preload=False)
```

### Step 3: Assign raw2 = read_raw_bti(...)

```python
raw2 = read_raw_bti(pdf, config, hs, convert=True, preload=False)
```

### Step 4: Call repr()

```python
repr(raw2)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(raw[:][0], raw2[:][0])
```

### Step 6: Assign pdf = BytesIO(...)

```python
pdf = BytesIO(fid.read())
```

### Step 7: Assign config = BytesIO(...)

```python
config = BytesIO(fid.read())
```

### Step 8: Assign hs = BytesIO(...)

```python
hs = BytesIO(fid.read())
```


## Complete Example

```python
# Setup
# Fixtures: pdf, config, hs, exported

# Workflow
'Test bti bytes-io API.'
raw = read_raw_bti(pdf, config, hs, convert=True, preload=False)
with open(pdf, 'rb') as fid:
    pdf = BytesIO(fid.read())
with open(config, 'rb') as fid:
    config = BytesIO(fid.read())
with open(hs, 'rb') as fid:
    hs = BytesIO(fid.read())
raw2 = read_raw_bti(pdf, config, hs, convert=True, preload=False)
repr(raw2)
assert_array_equal(raw[:][0], raw2[:][0])
```

## Next Steps


---

*Source: test_bti.py:360 | Complexity: Advanced | Last updated: 2026-05-18*