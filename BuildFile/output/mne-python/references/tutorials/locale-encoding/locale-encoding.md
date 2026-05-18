# How To: Locale Encoding

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test NIRx encoding.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test NIRx encoding.'

```python
'Test NIRx encoding.'
```

**Verification:**
```python
assert raw.info['meas_date'] == want_dt
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'latin'
```

### Step 3: Call copytree_rw()

```python
copytree_rw(fname_nirx_15_2, fname)
```

### Step 4: Assign hdr_fname = value

```python
hdr_fname = fname / 'NIRS-2019-10-02_003.hdr'
```

### Step 5: Assign hdr = list(...)

```python
hdr = list()
```

### Step 6: Assign unknown = b'Date="jeu. 13 f\xe9vr. 2020"\r\n'

```python
hdr[2] = b'Date="jeu. 13 f\xe9vr. 2020"\r\n'
```

### Step 7: Call read_raw_nirx()

```python
read_raw_nirx(fname, verbose='debug')
```

### Step 8: Assign unknown = b'Date="mi 13 dez 2020"\r\n'

```python
hdr[2] = b'Date="mi 13 dez 2020"\r\n'
```

### Step 9: Call read_raw_nirx()

```python
read_raw_nirx(fname, verbose='debug')
```

### Step 10: Assign unknown = b'Date="ven 24 gen 2020"\r\n'

```python
hdr[2] = b'Date="ven 24 gen 2020"\r\n'
```

### Step 11: Assign unknown = b'Time="10:57:41.454"\r\n'

```python
hdr[3] = b'Time="10:57:41.454"\r\n'
```

### Step 12: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname, verbose='debug')
```

### Step 13: Assign want_dt = dt.datetime(...)

```python
want_dt = dt.datetime(2020, 1, 24, 10, 57, 41, 454000, tzinfo=dt.timezone.utc)
```

**Verification:**
```python
assert raw.info['meas_date'] == want_dt
```

### Step 14: Call hdr.extend()

```python
hdr.extend((line for line in fid))
```

### Step 15: Call fid.write()

```python
fid.write(line)
```

### Step 16: Call fid.write()

```python
fid.write(line)
```

### Step 17: Call fid.write()

```python
fid.write(line)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test NIRx encoding.'
fname = tmp_path / 'latin'
copytree_rw(fname_nirx_15_2, fname)
hdr_fname = fname / 'NIRS-2019-10-02_003.hdr'
hdr = list()
with open(hdr_fname, 'rb') as fid:
    hdr.extend((line for line in fid))
hdr[2] = b'Date="jeu. 13 f\xe9vr. 2020"\r\n'
with open(hdr_fname, 'wb') as fid:
    for line in hdr:
        fid.write(line)
read_raw_nirx(fname, verbose='debug')
hdr[2] = b'Date="mi 13 dez 2020"\r\n'
with open(hdr_fname, 'wb') as fid:
    for line in hdr:
        fid.write(line)
read_raw_nirx(fname, verbose='debug')
hdr[2] = b'Date="ven 24 gen 2020"\r\n'
hdr[3] = b'Time="10:57:41.454"\r\n'
with open(hdr_fname, 'wb') as fid:
    for line in hdr:
        fid.write(line)
raw = read_raw_nirx(fname, verbose='debug')
want_dt = dt.datetime(2020, 1, 24, 10, 57, 41, 454000, tzinfo=dt.timezone.utc)
assert raw.info['meas_date'] == want_dt
```

## Next Steps


---

*Source: test_nirx.py:461 | Complexity: Advanced | Last updated: 2026-05-18*