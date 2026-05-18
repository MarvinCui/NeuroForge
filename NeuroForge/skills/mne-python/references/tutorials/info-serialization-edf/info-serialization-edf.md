# How To: Info Serialization Edf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Info JSON serialization with EDF data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test Info JSON serialization with EDF data.'

```python
'Test Info JSON serialization with EDF data.'
```

**Verification:**
```python
assert_object_equal(info, info_restored)
```

### Step 2: Assign edf_path = value

```python
edf_path = root_dir / 'io' / 'edf' / 'tests' / 'data' / 'test.edf'
```

### Step 3: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(edf_path, preload=False, verbose=False)
```

### Step 4: Assign info = raw.info.copy(...)

```python
info = raw.info.copy()
```

### Step 5: Assign json_path = value

```python
json_path = tmp_path / 'info_edf.json'
```

### Step 6: Assign info_restored = Info.from_json_dict(...)

```python
info_restored = Info.from_json_dict(info_dict)
```

### Step 7: Call assert_object_equal()

```python
assert_object_equal(info, info_restored)
```

### Step 8: Call json.dump()

```python
json.dump(info.to_json_dict(), f)
```

### Step 9: Assign info_dict = json.load(...)

```python
info_dict = json.load(f)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test Info JSON serialization with EDF data.'
edf_path = root_dir / 'io' / 'edf' / 'tests' / 'data' / 'test.edf'
raw = read_raw_edf(edf_path, preload=False, verbose=False)
info = raw.info.copy()
json_path = tmp_path / 'info_edf.json'
with open(json_path, 'w') as f:
    json.dump(info.to_json_dict(), f)
with open(json_path) as f:
    info_dict = json.load(f)
info_restored = Info.from_json_dict(info_dict)
assert_object_equal(info, info_restored)
```

## Next Steps


---

*Source: test_meas_info.py:379 | Complexity: Advanced | Last updated: 2026-05-18*