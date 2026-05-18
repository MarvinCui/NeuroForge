# How To: Filter Picks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test filter picking.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy.signal`
- `scipy.signal`
- `mne`
- `mne._fiff.pick`
- `mne.filter`
- `mne.io`
- `mne.utils`
- `mne.cuda`


## Step-by-Step Guide

### Step 1: 'Test filter picking.'

```python
'Test filter picking.'
```

**Verification:**
```python
assert_allclose(raw.get_data(), want)
```

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(3, 1000)
```

**Verification:**
```python
assert_allclose(raw.get_data(), want)
```

### Step 3: Assign fs = 1000.0

```python
fs = 1000.0
```

### Step 4: Assign kwargs = dict(...)

```python
kwargs = dict(l_freq=None, h_freq=40.0)
```

### Step 5: Assign filt = filter_data(...)

```python
filt = filter_data(data, fs, **kwargs)
```

### Step 6: Assign info = create_info(...)

```python
info = create_info(['s', 'k', 't'], fs, ['seeg', kind, 'stim'])
```

### Step 7: Assign raw = RawArray(...)

```python
raw = RawArray(data.copy(), info)
```

### Step 8: Call raw.filter()

```python
raw.filter(picks=picks, **kwargs)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw.get_data(), want)
```

### Step 10: Assign info = create_info(...)

```python
info = create_info(['k', 't'], fs, [kind, 'stim'])
```

### Step 11: Assign raw = RawArray(...)

```python
raw = RawArray(data[1:].copy(), info.copy())
```

### Step 12: Assign want = np.concatenate(...)

```python
want = np.concatenate((data[:1], filt[1:2], data[2:]))
```

### Step 13: Call raw.filter()

```python
raw.filter(picks=picks, **kwargs)
```

### Step 14: Assign want = value

```python
want = want[1:]
```

### Step 15: Call assert_allclose()

```python
assert_allclose(raw.get_data(), want)
```

### Step 16: Assign want = np.concatenate(...)

```python
want = np.concatenate((filt[:2], data[2:]))
```

### Step 17: Assign want = np.concatenate(...)

```python
want = np.concatenate((filt[:1], data[1:]))
```

### Step 18: Call raw.filter()

```python
raw.filter(picks=picks, **kwargs)
```


## Complete Example

```python
# Workflow
'Test filter picking.'
data = np.random.RandomState(0).randn(3, 1000)
fs = 1000.0
kwargs = dict(l_freq=None, h_freq=40.0)
filt = filter_data(data, fs, **kwargs)
for kind in ('eeg', 'grad', 'emg', 'misc', 'dbs'):
    for picks in (None, [-2], kind, 'k'):
        info = create_info(['s', 'k', 't'], fs, ['seeg', kind, 'stim'])
        raw = RawArray(data.copy(), info)
        raw.filter(picks=picks, **kwargs)
        if picks is None:
            if kind in _DATA_CH_TYPES_SPLIT:
                want = np.concatenate((filt[:2], data[2:]))
            else:
                want = np.concatenate((filt[:1], data[1:]))
        else:
            want = np.concatenate((data[:1], filt[1:2], data[2:]))
        assert_allclose(raw.get_data(), want)
        info = create_info(['k', 't'], fs, [kind, 'stim'])
        raw = RawArray(data[1:].copy(), info.copy())
        if picks is None and kind not in _DATA_CH_TYPES_SPLIT:
            with pytest.raises(ValueError, match='yielded no channels'):
                raw.filter(picks=picks, **kwargs)
        else:
            raw.filter(picks=picks, **kwargs)
            want = want[1:]
            assert_allclose(raw.get_data(), want)
```

## Next Steps


---

*Source: test_filter.py:1033 | Complexity: Advanced | Last updated: 2026-05-18*