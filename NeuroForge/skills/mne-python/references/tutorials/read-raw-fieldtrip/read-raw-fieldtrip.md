# How To: Read Raw Fieldtrip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test comparing reading a raw fiff file and the FieldTrip version.

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

### Step 1: 'Test comparing reading a raw fiff file and the FieldTrip version.'

```python
'Test comparing reading a raw fiff file and the FieldTrip version.'
```

### Step 2: Assign test_data_folder_ft = get_data_paths(...)

```python
test_data_folder_ft = get_data_paths(cur_system)
```

### Step 3: Assign raw_fiff_mne = get_raw_data(...)

```python
raw_fiff_mne = get_raw_data(cur_system, drop_extra_chs=True)
```

### Step 4: Assign cur_fname = value

```python
cur_fname = test_data_folder_ft / f'raw_{version}.mat'
```

### Step 5: Call check_data()

```python
check_data(raw_fiff_mne.get_data(), raw_fiff_ft.get_data(), cur_system)
```

### Step 6: Call check_info_fields()

```python
check_info_fields(raw_fiff_mne, raw_fiff_ft, use_info)
```

### Step 7: Assign info = get_raw_info(...)

```python
info = get_raw_info(cur_system)
```

### Step 8: Assign info = None

```python
info = None
```

### Step 9: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(**no_info_warning)
```

### Step 10: Assign raw_fiff_ft = mne.io.read_raw_fieldtrip(...)

```python
raw_fiff_ft = mne.io.read_raw_fieldtrip(cur_fname, info)
```

### Step 11: Call raw_fiff_ft.drop_channels()

```python
raw_fiff_ft.drop_channels(['MzA', 'MxA', 'MyaA', 'MyA', 'MxaA', 'MzaA'])
```

### Step 12: Call raw_fiff_ft.drop_channels()

```python
raw_fiff_ft.drop_channels(['TRIG2', 'TRIG1', 'GATE'])
```

### Step 13: Call _test_raw_reader()

```python
_test_raw_reader(read_raw_fieldtrip, fname=cur_fname, info=info, test_preloading=False, test_kwargs=False)
```

### Step 14: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(RuntimeWarning, match='cannot be found in')
```

### Step 15: Assign ctx = nullcontext(...)

```python
ctx = nullcontext()
```


## Complete Example

```python
# Setup
# Fixtures: cur_system, version, use_info

# Workflow
'Test comparing reading a raw fiff file and the FieldTrip version.'
test_data_folder_ft = get_data_paths(cur_system)
raw_fiff_mne = get_raw_data(cur_system, drop_extra_chs=True)
if use_info:
    info = get_raw_info(cur_system)
    if cur_system in ('BTI', 'eximia'):
        ctx = pytest.warns(RuntimeWarning, match='cannot be found in')
    else:
        ctx = nullcontext()
else:
    info = None
    ctx = pytest.warns(**no_info_warning)
cur_fname = test_data_folder_ft / f'raw_{version}.mat'
with _record_warnings(), ctx:
    raw_fiff_ft = mne.io.read_raw_fieldtrip(cur_fname, info)
if cur_system == 'BTI' and (not use_info):
    raw_fiff_ft.drop_channels(['MzA', 'MxA', 'MyaA', 'MyA', 'MxaA', 'MzaA'])
if cur_system == 'eximia' and (not use_info):
    raw_fiff_ft.drop_channels(['TRIG2', 'TRIG1', 'GATE'])
check_data(raw_fiff_mne.get_data(), raw_fiff_ft.get_data(), cur_system)
with _record_warnings():
    _test_raw_reader(read_raw_fieldtrip, fname=cur_fname, info=info, test_preloading=False, test_kwargs=False)
check_info_fields(raw_fiff_mne, raw_fiff_ft, use_info)
```

## Next Steps


---

*Source: test_fieldtrip.py:141 | Complexity: Advanced | Last updated: 2026-05-18*