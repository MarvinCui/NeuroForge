# How To: Persyst Annotations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test annotations reading in Persyst.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test annotations reading in Persyst.'

```python
'Test annotations reading in Persyst.'
```

**Verification:**
```python
assert np.count_nonzero(annotations.description == 'seizure') == 2
```

### Step 2: Assign new_fname_lay = value

```python
new_fname_lay = tmp_path / fname_lay.name
```

**Verification:**
```python
assert 'seizure1,2' in annotations.description
```

### Step 3: Assign new_fname_dat = value

```python
new_fname_dat = tmp_path / fname_dat.name
```

**Verification:**
```python
assert 'CLip2' in annotations.description
```

### Step 4: Call shutil.copy()

```python
shutil.copy(fname_dat, new_fname_dat)
```

### Step 5: Call shutil.copy()

```python
shutil.copy(fname_lay, new_fname_lay)
```

### Step 6: Assign raw = read_raw_persyst(...)

```python
raw = read_raw_persyst(new_fname_lay)
```

### Step 7: Call raw.crop()

```python
raw.crop(tmin=0, tmax=4)
```

### Step 8: Assign annotations = value

```python
annotations = raw.annotations
```

**Verification:**
```python
assert np.count_nonzero(annotations.description == 'seizure') == 2
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test annotations reading in Persyst.'
new_fname_lay = tmp_path / fname_lay.name
new_fname_dat = tmp_path / fname_dat.name
shutil.copy(fname_dat, new_fname_dat)
shutil.copy(fname_lay, new_fname_lay)
raw = read_raw_persyst(new_fname_lay)
raw.crop(tmin=0, tmax=4)
annotations = raw.annotations
assert np.count_nonzero(annotations.description == 'seizure') == 2
assert 'seizure1,2' in annotations.description
assert 'CLip2' in annotations.description
```

## Next Steps


---

*Source: test_persyst.py:192 | Complexity: Advanced | Last updated: 2026-05-18*