# How To: Read Evoked

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test comparing reading an Evoked object and the FieldTrip version.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `itertools`
- `contextlib`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.fieldtrip.tests.helpers`
- `mne.io.fieldtrip.utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: cur_system, version, use_info
```

## Step-by-Step Guide

### Step 1: 'Test comparing reading an Evoked object and the FieldTrip version.'

```python
'Test comparing reading an Evoked object and the FieldTrip version.'
```

### Step 2: Assign test_data_folder_ft = get_data_paths(...)

```python
test_data_folder_ft = get_data_paths(cur_system)
```

### Step 3: Assign mne_avg = get_evoked(...)

```python
mne_avg = get_evoked(cur_system)
```

### Step 4: Assign cur_fname = value

```python
cur_fname = test_data_folder_ft / f'averaged_{version}.mat'
```

### Step 5: Assign mne_data = value

```python
mne_data = mne_avg.data[:, :-1]
```

### Step 6: Assign ft_data = value

```python
ft_data = avg_ft.data
```

### Step 7: Call check_data()

```python
check_data(mne_data, ft_data, cur_system)
```

### Step 8: Call check_info_fields()

```python
check_info_fields(mne_avg, avg_ft, use_info)
```

### Step 9: Assign info = get_raw_info(...)

```python
info = get_raw_info(cur_system)
```

### Step 10: Assign avg_ft = mne.io.read_evoked_fieldtrip(...)

```python
avg_ft = mne.io.read_evoked_fieldtrip(cur_fname, info)
```

### Step 11: Assign info = None

```python
info = None
```

### Step 12: Assign avg_ft = mne.io.read_evoked_fieldtrip(...)

```python
avg_ft = mne.io.read_evoked_fieldtrip(cur_fname, info)
```


## Complete Example

```python
# Setup
# Fixtures: cur_system, version, use_info

# Workflow
'Test comparing reading an Evoked object and the FieldTrip version.'
test_data_folder_ft = get_data_paths(cur_system)
mne_avg = get_evoked(cur_system)
cur_fname = test_data_folder_ft / f'averaged_{version}.mat'
if use_info:
    info = get_raw_info(cur_system)
    avg_ft = mne.io.read_evoked_fieldtrip(cur_fname, info)
else:
    info = None
    with _record_warnings(), pytest.warns(**no_info_warning):
        avg_ft = mne.io.read_evoked_fieldtrip(cur_fname, info)
mne_data = mne_avg.data[:, :-1]
ft_data = avg_ft.data
check_data(mne_data, ft_data, cur_system)
check_info_fields(mne_avg, avg_ft, use_info)
```

## Next Steps


---

*Source: test_fieldtrip.py:64 | Complexity: Advanced | Last updated: 2026-05-18*