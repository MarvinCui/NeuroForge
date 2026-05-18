# How To: Sleep Physionet Age

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test Sleep Physionet URL handling.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `pytest`
- `mne.datasets.sleep_physionet`
- `mne.datasets.sleep_physionet._utils`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: physionet_tmpdir, fake_retrieve
```

## Step-by-Step Guide

### Step 1: 'Test Sleep Physionet URL handling.'

```python
'Test Sleep Physionet URL handling.'
```

**Verification:**
```python
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
```

### Step 2: Assign paths = age.fetch_data(...)

```python
paths = age.fetch_data(subjects=[0], recording=[1], path=physionet_tmpdir)
```

**Verification:**
```python
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
```

### Step 3: Assign paths = age.fetch_data(...)

```python
paths = age.fetch_data(subjects=[0, 1], recording=[1], path=physionet_tmpdir)
```

**Verification:**
```python
assert _keep_basename_only(paths[1]) == ['SC4011E0-PSG.edf', 'SC4011EH-Hypnogram.edf']
```

### Step 4: Assign paths = age.fetch_data(...)

```python
paths = age.fetch_data(subjects=[0], recording=[1, 2], path=physionet_tmpdir)
```

**Verification:**
```python
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
```

### Step 5: Assign EXPECTED_CALLS = value

```python
EXPECTED_CALLS = ({'name': 'SC4001E0-PSG.edf', 'hash': 'adabd3b01fc7bb75c523a974f38ee3ae4e57b40f'}, {'name': 'SC4001EC-Hypnogram.edf', 'hash': '21c998eadc8b1e3ea6727d3585186b8f76e7e70b'}, {'name': 'SC4011E0-PSG.edf', 'hash': '4d17451f7847355bcab17584de05e7e1df58c660'}, {'name': 'SC4011EH-Hypnogram.edf', 'hash': 'd582a3cbe2db481a362af890bc5a2f5ca7c878dc'}, {'name': 'SC4002E0-PSG.edf', 'hash': 'c6b6d7a8605cc7e7602b6028ee77f6fbf5f7581d'}, {'name': 'SC4002EC-Hypnogram.edf', 'hash': '386230188a3552b1fc90bba0fb7476ceaca174b6'})
```

**Verification:**
```python
assert _keep_basename_only(paths[1]) == ['SC4002E0-PSG.edf', 'SC4002EC-Hypnogram.edf']
```

### Step 6: Assign base_path = age.data_path(...)

```python
base_path = age.data_path(path=physionet_tmpdir)
```

### Step 7: Call _check_mocked_function_calls()

```python
_check_mocked_function_calls(fake_retrieve, EXPECTED_CALLS, base_path)
```


## Complete Example

```python
# Setup
# Fixtures: physionet_tmpdir, fake_retrieve

# Workflow
'Test Sleep Physionet URL handling.'
paths = age.fetch_data(subjects=[0], recording=[1], path=physionet_tmpdir)
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
paths = age.fetch_data(subjects=[0, 1], recording=[1], path=physionet_tmpdir)
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
assert _keep_basename_only(paths[1]) == ['SC4011E0-PSG.edf', 'SC4011EH-Hypnogram.edf']
paths = age.fetch_data(subjects=[0], recording=[1, 2], path=physionet_tmpdir)
assert _keep_basename_only(paths[0]) == ['SC4001E0-PSG.edf', 'SC4001EC-Hypnogram.edf']
assert _keep_basename_only(paths[1]) == ['SC4002E0-PSG.edf', 'SC4002EC-Hypnogram.edf']
EXPECTED_CALLS = ({'name': 'SC4001E0-PSG.edf', 'hash': 'adabd3b01fc7bb75c523a974f38ee3ae4e57b40f'}, {'name': 'SC4001EC-Hypnogram.edf', 'hash': '21c998eadc8b1e3ea6727d3585186b8f76e7e70b'}, {'name': 'SC4011E0-PSG.edf', 'hash': '4d17451f7847355bcab17584de05e7e1df58c660'}, {'name': 'SC4011EH-Hypnogram.edf', 'hash': 'd582a3cbe2db481a362af890bc5a2f5ca7c878dc'}, {'name': 'SC4002E0-PSG.edf', 'hash': 'c6b6d7a8605cc7e7602b6028ee77f6fbf5f7581d'}, {'name': 'SC4002EC-Hypnogram.edf', 'hash': '386230188a3552b1fc90bba0fb7476ceaca174b6'})
base_path = age.data_path(path=physionet_tmpdir)
_check_mocked_function_calls(fake_retrieve, EXPECTED_CALLS, base_path)
```

## Next Steps


---

*Source: test_physionet.py:121 | Complexity: Intermediate | Last updated: 2026-05-18*