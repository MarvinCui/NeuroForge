# How To: Pick Channels Cov

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking channels from a Covariance object.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test picking channels from a Covariance object.'

```python
'Test picking channels from a Covariance object.'
```

**Verification:**
```python
assert cov_copy.ch_names == ['CH1', 'CH2']
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(['CH1', 'CH2', 'CH3'], 1.0, ch_types='eeg')
```

**Verification:**
```python
assert_array_equal(cov_copy['data'], [1.0, 2.0])
```

### Step 3: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(info)
```

**Verification:**
```python
assert cov_copy.ch_names == ['CH2', 'CH1']
```

### Step 4: Assign unknown = np.array(...)

```python
cov['data'] = np.array([1.0, 2.0, 3.0])
```

**Verification:**
```python
assert_array_equal(cov_copy['data'], [2.0, 1.0])
```

### Step 5: Assign cov_copy = pick_channels_cov(...)

```python
cov_copy = pick_channels_cov(cov, ['CH2', 'CH1'], ordered=False, copy=True)
```

**Verification:**
```python
assert cov.ch_names == ['CH1', 'CH2']
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(cov_copy['data'], [1.0, 2.0])
```

**Verification:**
```python
assert_array_equal(cov['data'], [1.0, 2.0])
```

### Step 7: Assign cov_copy = pick_channels_cov(...)

```python
cov_copy = pick_channels_cov(cov, ['CH2', 'CH1'], ordered=True, copy=True)
```

**Verification:**
```python
assert 'method' not in cov_copy
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(cov_copy['data'], [2.0, 1.0])
```

**Verification:**
```python
assert 'loglik' not in cov_copy
```

### Step 9: Call pick_channels_cov()

```python
pick_channels_cov(cov, ['CH2', 'CH1'], copy=False, ordered=False)
```

**Verification:**
```python
assert cov.ch_names == ['CH1', 'CH2']
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(cov['data'], [1.0, 2.0])
```

### Step 11: Assign unknown = None

```python
cov['method'] = None
```

### Step 12: Assign unknown = None

```python
cov['loglik'] = None
```

### Step 13: Assign cov_copy = pick_channels_cov(...)

```python
cov_copy = pick_channels_cov(cov, ['CH1', 'CH2'], copy=True)
```

**Verification:**
```python
assert 'method' not in cov_copy
```


## Complete Example

```python
# Workflow
'Test picking channels from a Covariance object.'
info = create_info(['CH1', 'CH2', 'CH3'], 1.0, ch_types='eeg')
cov = make_ad_hoc_cov(info)
cov['data'] = np.array([1.0, 2.0, 3.0])
cov_copy = pick_channels_cov(cov, ['CH2', 'CH1'], ordered=False, copy=True)
assert cov_copy.ch_names == ['CH1', 'CH2']
assert_array_equal(cov_copy['data'], [1.0, 2.0])
cov_copy = pick_channels_cov(cov, ['CH2', 'CH1'], ordered=True, copy=True)
assert cov_copy.ch_names == ['CH2', 'CH1']
assert_array_equal(cov_copy['data'], [2.0, 1.0])
pick_channels_cov(cov, ['CH2', 'CH1'], copy=False, ordered=False)
assert cov.ch_names == ['CH1', 'CH2']
assert_array_equal(cov['data'], [1.0, 2.0])
cov['method'] = None
cov['loglik'] = None
cov_copy = pick_channels_cov(cov, ['CH1', 'CH2'], copy=True)
assert 'method' not in cov_copy
assert 'loglik' not in cov_copy
```

## Next Steps


---

*Source: test_pick.py:677 | Complexity: Advanced | Last updated: 2026-05-18*