# How To: Nan Interpolation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test 'nan' method for interpolating bads.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.channels`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne.channels`
- `mne.channels.interpolation`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`
- `mne.channels.interpolation`

**Setup Required:**
```python
# Fixtures: raw
```

## Step-by-Step Guide

### Step 1: "Test 'nan' method for interpolating bads."

```python
"Test 'nan' method for interpolating bads."
```

**Verification:**
```python
assert np.isnan(bad_chs).all()
```

### Step 2: Assign ch_to_interp = value

```python
ch_to_interp = [raw.ch_names[1]]
```

**Verification:**
```python
assert raw.info['bads'] == ch_to_interp
```

### Step 3: Assign unknown = ch_to_interp

```python
raw.info['bads'] = ch_to_interp
```

**Verification:**
```python
assert raw.interpolate_bads(on_bad_position='ignore')
```

### Step 4: Assign bad_chs = raw.get_data(...)

```python
bad_chs = raw.get_data(ch_to_interp)
```

**Verification:**
```python
assert np.isnan(bad_chs).all, 'Interpolated channel should be all NaN'
```

### Step 5: Assign unknown = ch_to_interp

```python
raw.info['bads'] = ch_to_interp
```

**Verification:**
```python
assert np.isfinite(good_chs).all()
```

### Step 6: Call raw.interpolate_bads()

```python
raw.interpolate_bads(method='nan', reset_bads=False)
```

**Verification:**
```python
assert raw.info['bads'] == ch_to_interp
```

### Step 7: Assign store = value

```python
store = raw.info['chs'][1]['loc']
```

### Step 8: Assign unknown = ch_to_interp

```python
raw.info['bads'] = ch_to_interp
```

### Step 9: Assign unknown = np.full(...)

```python
raw.info['chs'][1]['loc'] = np.full(12, np.nan)
```

### Step 10: Assign unknown = ch_to_interp

```python
raw.info['bads'] = ch_to_interp
```

**Verification:**
```python
assert raw.interpolate_bads(on_bad_position='ignore')
```

### Step 11: Assign unknown = store

```python
raw.info['chs'][1]['loc'] = store
```

### Step 12: Call raw.drop_channels()

```python
raw.drop_channels(ch_to_interp)
```

### Step 13: Assign good_chs = raw.get_data(...)

```python
good_chs = raw.get_data()
```

**Verification:**
```python
assert np.isfinite(good_chs).all()
```

### Step 14: Call raw.interpolate_bads()

```python
raw.interpolate_bads(method='nan', reset_bads=True)
```

### Step 15: Call raw.interpolate_bads()

```python
raw.interpolate_bads(on_bad_position='raise')
```

### Step 16: Call raw.interpolate_bads()

```python
raw.interpolate_bads(on_bad_position='warn')
```


## Complete Example

```python
# Setup
# Fixtures: raw

# Workflow
"Test 'nan' method for interpolating bads."
ch_to_interp = [raw.ch_names[1]]
raw.info['bads'] = ch_to_interp
with pytest.warns(RuntimeWarning, match='Consider setting reset_bads=False'):
    raw.interpolate_bads(method='nan', reset_bads=True)
bad_chs = raw.get_data(ch_to_interp)
assert np.isnan(bad_chs).all()
raw.info['bads'] = ch_to_interp
raw.interpolate_bads(method='nan', reset_bads=False)
assert raw.info['bads'] == ch_to_interp
store = raw.info['chs'][1]['loc']
raw.info['bads'] = ch_to_interp
raw.info['chs'][1]['loc'] = np.full(12, np.nan)
with pytest.raises(ValueError, match='have invalid sensor position'):
    raw.interpolate_bads(on_bad_position='raise')
with pytest.warns(RuntimeWarning, match='have invalid sensor position'):
    raw.interpolate_bads(on_bad_position='warn')
raw.info['bads'] = ch_to_interp
assert raw.interpolate_bads(on_bad_position='ignore')
assert np.isnan(bad_chs).all, 'Interpolated channel should be all NaN'
raw.info['chs'][1]['loc'] = store
raw.drop_channels(ch_to_interp)
good_chs = raw.get_data()
assert np.isfinite(good_chs).all()
```

## Next Steps


---

*Source: test_interpolation.py:444 | Complexity: Advanced | Last updated: 2026-05-18*