# How To: Gdf2 Birthday

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading raw GDF 2.x files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `datetime`
- `io`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading raw GDF 2.x files.'

```python
'Test reading raw GDF 2.x files.'
```

**Verification:**
```python
assert np.fromfile(fid, np.uint64, 1)[0] == 0
```

### Step 2: Assign new_fname = value

```python
new_fname = tmp_path / 'temp.gdf'
```

**Verification:**
```python
assert np.fromfile(fid, np.uint64, 1)[0] == d
```

### Step 3: Call shutil.copyfile()

```python
shutil.copyfile(gdf2_path.with_name(gdf2_path.name + '.gdf'), new_fname)
```

**Verification:**
```python
assert 'subject_info' not in raw._raw_extras[0]
```

### Step 4: Assign offset_edf = value

```python
offset_edf = datetime.now(tz=timezone.utc) - datetime(1, 1, 1, tzinfo=timezone.utc)
```

**Verification:**
```python
assert raw.info['subject_info'] is not None
```

### Step 5: Assign offset_44_yr = value

```python
offset_44_yr = offset_edf - timedelta(days=int(365 * 44.5))
```

**Verification:**
```python
assert raw.info['subject_info']['birthday'] == date(birthdate.year, birthdate.month, birthdate.day)
```

### Step 6: Assign offset_44_yr_days = value

```python
offset_44_yr_days = offset_44_yr.total_seconds() / (24 * 60 * 60)
```

### Step 7: Assign d = value

```python
d = (int(offset_44_yr_days) + 367) * 2 ** 32
```

### Step 8: Assign raw = read_raw_gdf(...)

```python
raw = read_raw_gdf(new_fname, eog=None, misc=None, preload=True)
```

**Verification:**
```python
assert 'subject_info' not in raw._raw_extras[0]
```

### Step 9: Assign birthdate = value

```python
birthdate = datetime(1, 1, 1, tzinfo=timezone.utc) + offset_44_yr
```

**Verification:**
```python
assert raw.info['subject_info']['birthday'] == date(birthdate.year, birthdate.month, birthdate.day)
```

### Step 10: Call fid.seek()

```python
fid.seek(176, 0)
```

**Verification:**
```python
assert np.fromfile(fid, np.uint64, 1)[0] == 0
```

### Step 11: Call fid.seek()

```python
fid.seek(176, 0)
```

### Step 12: Call fid.write()

```python
fid.write(np.array([d], np.uint64).tobytes())
```

### Step 13: Call fid.seek()

```python
fid.seek(176, 0)
```

**Verification:**
```python
assert np.fromfile(fid, np.uint64, 1)[0] == d
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading raw GDF 2.x files.'
new_fname = tmp_path / 'temp.gdf'
shutil.copyfile(gdf2_path.with_name(gdf2_path.name + '.gdf'), new_fname)
offset_edf = datetime.now(tz=timezone.utc) - datetime(1, 1, 1, tzinfo=timezone.utc)
offset_44_yr = offset_edf - timedelta(days=int(365 * 44.5))
offset_44_yr_days = offset_44_yr.total_seconds() / (24 * 60 * 60)
d = (int(offset_44_yr_days) + 367) * 2 ** 32
with open(new_fname, 'r+b') as fid:
    fid.seek(176, 0)
    assert np.fromfile(fid, np.uint64, 1)[0] == 0
    fid.seek(176, 0)
    fid.write(np.array([d], np.uint64).tobytes())
    fid.seek(176, 0)
    assert np.fromfile(fid, np.uint64, 1)[0] == d
raw = read_raw_gdf(new_fname, eog=None, misc=None, preload=True)
assert 'subject_info' not in raw._raw_extras[0]
assert raw.info['subject_info'] is not None
birthdate = datetime(1, 1, 1, tzinfo=timezone.utc) + offset_44_yr
assert raw.info['subject_info']['birthday'] == date(birthdate.year, birthdate.month, birthdate.day)
```

## Next Steps


---

*Source: test_gdf.py:83 | Complexity: Advanced | Last updated: 2026-05-18*