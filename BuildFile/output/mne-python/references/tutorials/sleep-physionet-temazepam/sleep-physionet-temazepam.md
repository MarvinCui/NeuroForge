# How To: Sleep Physionet Temazepam

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
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
assert _keep_basename_only(paths[0]) == ['ST7011J0-PSG.edf', 'ST7011JP-Hypnogram.edf']
```

### Step 2: Assign paths = temazepam.fetch_data(...)

```python
paths = temazepam.fetch_data(subjects=[0], path=physionet_tmpdir)
```

**Verification:**
```python
assert _keep_basename_only(paths[0]) == ['ST7011J0-PSG.edf', 'ST7011JP-Hypnogram.edf']
```

### Step 3: Assign EXPECTED_CALLS = value

```python
EXPECTED_CALLS = ({'name': 'ST7011J0-PSG.edf', 'hash': 'b9d11484126ebff1884034396d6a20c62c0ef48d'}, {'name': 'ST7011JP-Hypnogram.edf', 'hash': 'ff28e5e01296cefed49ae0c27cfb3ebc42e710bf'})
```

### Step 4: Assign base_path = temazepam.data_path(...)

```python
base_path = temazepam.data_path(path=physionet_tmpdir)
```

### Step 5: Call _check_mocked_function_calls()

```python
_check_mocked_function_calls(fake_retrieve, EXPECTED_CALLS, base_path)
```

### Step 6: Assign paths = temazepam.fetch_data(...)

```python
paths = temazepam.fetch_data(subjects=[22], path=physionet_tmpdir)
```


## Complete Example

```python
# Setup
# Fixtures: physionet_tmpdir, fake_retrieve

# Workflow
'Test Sleep Physionet URL handling.'
paths = temazepam.fetch_data(subjects=[0], path=physionet_tmpdir)
assert _keep_basename_only(paths[0]) == ['ST7011J0-PSG.edf', 'ST7011JP-Hypnogram.edf']
EXPECTED_CALLS = ({'name': 'ST7011J0-PSG.edf', 'hash': 'b9d11484126ebff1884034396d6a20c62c0ef48d'}, {'name': 'ST7011JP-Hypnogram.edf', 'hash': 'ff28e5e01296cefed49ae0c27cfb3ebc42e710bf'})
base_path = temazepam.data_path(path=physionet_tmpdir)
_check_mocked_function_calls(fake_retrieve, EXPECTED_CALLS, base_path)
with pytest.raises(ValueError, match='This dataset contains subjects 0 to 21'):
    paths = temazepam.fetch_data(subjects=[22], path=physionet_tmpdir)
```

## Next Steps


---

*Source: test_physionet.py:192 | Complexity: Intermediate | Last updated: 2026-05-18*