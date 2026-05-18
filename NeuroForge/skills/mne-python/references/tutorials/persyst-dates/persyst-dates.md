# How To: Persyst Dates

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test different Persyst date formats for meas date.

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

### Step 1: 'Test different Persyst date formats for meas date.'

```python
'Test different Persyst date formats for meas date.'
```

**Verification:**
```python
assert raw.info['meas_date'].month == 1
```

### Step 2: Assign new_fname_lay = value

```python
new_fname_lay = tmp_path / fname_lay.name
```

**Verification:**
```python
assert raw.info['meas_date'].day == 23
```

### Step 3: Assign new_fname_dat = value

```python
new_fname_dat = tmp_path / fname_dat.name
```

**Verification:**
```python
assert raw.info['meas_date'].year == 2000
```

### Step 4: Call shutil.copy()

```python
shutil.copy(fname_dat, new_fname_dat)
```

**Verification:**
```python
assert raw.info['meas_date'].month == 1
```

### Step 5: Assign raw = read_raw_persyst(...)

```python
raw = read_raw_persyst(new_fname_lay)
```

**Verification:**
```python
assert raw.info['meas_date'].day == 24
```

### Step 6: Call os.remove()

```python
os.remove(new_fname_lay)
```

**Verification:**
```python
assert raw.info['meas_date'].year == 2000
```

### Step 7: Assign raw = read_raw_persyst(...)

```python
raw = read_raw_persyst(new_fname_lay)
```

**Verification:**
```python
assert raw.info['meas_date'].month == 1
```

### Step 8: Call fout.write()

```python
fout.write(line)
```

### Step 9: Call fout.write()

```python
fout.write(line)
```

### Step 10: Assign line = 'TestDate=01/23/2000\n'

```python
line = 'TestDate=01/23/2000\n'
```

### Step 11: Assign line = 'TestDate=24-01-2000\n'

```python
line = 'TestDate=24-01-2000\n'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test different Persyst date formats for meas date.'
new_fname_lay = tmp_path / fname_lay.name
new_fname_dat = tmp_path / fname_dat.name
shutil.copy(fname_dat, new_fname_dat)
with open(fname_lay) as fin:
    with open(new_fname_lay, 'w') as fout:
        for idx, line in enumerate(fin):
            if line.startswith('TestDate'):
                line = 'TestDate=01/23/2000\n'
            fout.write(line)
raw = read_raw_persyst(new_fname_lay)
assert raw.info['meas_date'].month == 1
assert raw.info['meas_date'].day == 23
assert raw.info['meas_date'].year == 2000
os.remove(new_fname_lay)
with open(fname_lay) as fin:
    with open(new_fname_lay, 'w') as fout:
        for idx, line in enumerate(fin):
            if line.startswith('TestDate'):
                line = 'TestDate=24-01-2000\n'
            fout.write(line)
raw = read_raw_persyst(new_fname_lay)
assert raw.info['meas_date'].month == 1
assert raw.info['meas_date'].day == 24
assert raw.info['meas_date'].year == 2000
```

## Next Steps


---

*Source: test_persyst.py:79 | Complexity: Advanced | Last updated: 2026-05-18*