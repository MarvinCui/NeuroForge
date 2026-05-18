# How To: Create Events

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test 2dim trialinfo fields.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test 2dim trialinfo fields.'

```python
'Test 2dim trialinfo fields.'
```

**Verification:**
```python
assert np.all(evts[:, 2] == cur_col + 1)
```

### Step 2: Assign test_data_folder_ft = get_data_paths(...)

```python
test_data_folder_ft = get_data_paths('neuromag306')
```

### Step 3: Assign cur_fname = value

```python
cur_fname = test_data_folder_ft / 'epoched_v7.mat'
```

### Step 4: Assign original_data = pymatreader.read_mat(...)

```python
original_data = pymatreader.read_mat(cur_fname, ['data'])
```

### Step 5: Assign new_data = copy.deepcopy(...)

```python
new_data = copy.deepcopy(original_data)
```

### Step 6: Assign unknown = np.array(...)

```python
new_data['trialinfo'] = np.array([[1, 2, 3, 4], [1, 2, 3, 4], [1, 2, 3, 4]])
```

### Step 7: Call _create_events()

```python
_create_events(new_data, -1)
```

### Step 8: Assign evts = _create_events(...)

```python
evts = _create_events(new_data, cur_col)
```

**Verification:**
```python
assert np.all(evts[:, 2] == cur_col + 1)
```

### Step 9: Call _create_events()

```python
_create_events(new_data, 4)
```


## Complete Example

```python
# Workflow
'Test 2dim trialinfo fields.'
test_data_folder_ft = get_data_paths('neuromag306')
cur_fname = test_data_folder_ft / 'epoched_v7.mat'
original_data = pymatreader.read_mat(cur_fname, ['data'])
new_data = copy.deepcopy(original_data)
new_data['trialinfo'] = np.array([[1, 2, 3, 4], [1, 2, 3, 4], [1, 2, 3, 4]])
with pytest.raises(ValueError):
    _create_events(new_data, -1)
for cur_col in np.arange(4):
    evts = _create_events(new_data, cur_col)
    assert np.all(evts[:, 2] == cur_col + 1)
with pytest.raises(ValueError):
    _create_events(new_data, 4)
```

## Next Steps


---

*Source: test_fieldtrip.py:210 | Complexity: Advanced | Last updated: 2026-05-18*