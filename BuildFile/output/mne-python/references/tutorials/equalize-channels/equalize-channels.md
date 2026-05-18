# How To: Equalize Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test equalizing channels and their ordering.

## Prerequisites

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test equalizing channels and their ordering.'

```python
'Test equalizing channels and their ordering.'
```

**Verification:**
```python
assert raw2.ch_names == ['CH1', 'CH2']
```

### Step 2: Call pytest.raises()

```python
pytest.raises(TypeError, equalize_channels, ['foo', 'bar'], match='Instances to be modified must be an instance of')
```

**Verification:**
```python
assert_array_equal(raw2.get_data(), [[1.0], [2.0]])
```

### Step 3: Assign raw = RawArray(...)

```python
raw = RawArray([[1.0], [2.0], [3.0], [4.0]], create_info(['CH1', 'CH2', 'CH3', 'CH4'], sfreq=1.0))
```

**Verification:**
```python
assert epochs2.ch_names == ['CH1', 'CH2']
```

### Step 4: Assign epochs = EpochsArray(...)

```python
epochs = EpochsArray([[[1.0], [2.0], [3.0]]], create_info(['CH5', 'CH2', 'CH1'], sfreq=1.0))
```

**Verification:**
```python
assert_array_equal(epochs2.get_data(copy=False), [[[3.0], [2.0]]])
```

### Step 5: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(create_info(['CH2', 'CH1', 'CH8'], sfreq=1.0, ch_types='eeg'))
```

**Verification:**
```python
assert cov2.ch_names == ['CH1', 'CH2']
```

### Step 6: Assign unknown = value

```python
cov['bads'] = ['CH1']
```

**Verification:**
```python
assert cov2['bads'] == cov['bads']
```

### Step 7: Assign ave = EvokedArray(...)

```python
ave = EvokedArray([[1.0], [2.0]], create_info(['CH1', 'CH2'], sfreq=1.0))
```

**Verification:**
```python
assert ave2.ch_names == ave.ch_names
```

### Step 8: Assign unknown = equalize_channels(...)

```python
raw2, epochs2, cov2, ave2 = equalize_channels([raw, epochs, cov, ave], copy=True)
```

**Verification:**
```python
assert_array_equal(ave2.data, ave.data)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(raw2.get_data(), [[1.0], [2.0]])
```

**Verification:**
```python
assert raw is not raw2
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(epochs2.get_data(copy=False), [[[3.0], [2.0]]])
```

**Verification:**
```python
assert epochs is not epochs2
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(ave2.data, ave.data)
```

**Verification:**
```python
assert cov is not cov2
```

### Step 12: Assign unknown = equalize_channels(...)

```python
raw2, epochs2 = equalize_channels([raw, epochs], copy=False)
```

**Verification:**
```python
assert ave is ave2
```


## Complete Example

```python
# Workflow
'Test equalizing channels and their ordering.'
pytest.raises(TypeError, equalize_channels, ['foo', 'bar'], match='Instances to be modified must be an instance of')
raw = RawArray([[1.0], [2.0], [3.0], [4.0]], create_info(['CH1', 'CH2', 'CH3', 'CH4'], sfreq=1.0))
epochs = EpochsArray([[[1.0], [2.0], [3.0]]], create_info(['CH5', 'CH2', 'CH1'], sfreq=1.0))
cov = make_ad_hoc_cov(create_info(['CH2', 'CH1', 'CH8'], sfreq=1.0, ch_types='eeg'))
cov['bads'] = ['CH1']
ave = EvokedArray([[1.0], [2.0]], create_info(['CH1', 'CH2'], sfreq=1.0))
raw2, epochs2, cov2, ave2 = equalize_channels([raw, epochs, cov, ave], copy=True)
assert raw2.ch_names == ['CH1', 'CH2']
assert_array_equal(raw2.get_data(), [[1.0], [2.0]])
assert epochs2.ch_names == ['CH1', 'CH2']
assert_array_equal(epochs2.get_data(copy=False), [[[3.0], [2.0]]])
assert cov2.ch_names == ['CH1', 'CH2']
assert cov2['bads'] == cov['bads']
assert ave2.ch_names == ave.ch_names
assert_array_equal(ave2.data, ave.data)
assert raw is not raw2
assert epochs is not epochs2
assert cov is not cov2
assert ave is ave2
raw2, epochs2 = equalize_channels([raw, epochs], copy=False)
assert raw is raw2
assert epochs is epochs2
```

## Next Steps


---

*Source: test_channels.py:562 | Complexity: Advanced | Last updated: 2026-05-18*