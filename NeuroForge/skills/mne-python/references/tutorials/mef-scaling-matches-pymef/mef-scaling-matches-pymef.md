# How To: Mef Scaling Matches Pymef

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that MNE scaling matches pymef data plus metadata scaling.

## Prerequisites

**Required Modules:**
- `types`
- `numpy`
- `pytest`
- `mne.datasets`
- `mne.io`
- `mne.io.mef._utils`


## Step-by-Step Guide

### Step 1: 'Test that MNE scaling matches pymef data plus metadata scaling.'

```python
'Test that MNE scaling matches pymef data plus metadata scaling.'
```

**Verification:**
```python
assert not np.allclose(scales, 1)
```

### Step 2: Assign raw = read_raw_mef(...)

```python
raw = read_raw_mef(mef_file_path, preload=False)
```

### Step 3: Assign session = pymef.mef_session.MefSession(...)

```python
session = pymef.mef_session.MefSession(str(mef_file_path), '')
```

### Step 4: Assign ts_channels = value

```python
ts_channels = session.session_md['time_series_channels']
```

### Step 5: Assign scales = value

```python
scales = []
```

### Step 6: Assign scales = np.array(...)

```python
scales = np.array(scales)
```

**Verification:**
```python
assert not np.allclose(scales, 1)
```

### Step 7: Assign unknown = value

```python
start, stop = (0, 10)
```

### Step 8: Assign pymef_data = session.read_ts_channels_sample(...)

```python
pymef_data = session.read_ts_channels_sample(raw.ch_names, [start, stop])
```

### Step 9: Assign pymef_data = np.array(...)

```python
pymef_data = np.array(pymef_data, dtype=np.float64)
```

### Step 10: Assign expected = value

```python
expected = pymef_data * scales[:, np.newaxis]
```

### Step 11: Assign data = raw.get_data(...)

```python
data = raw.get_data(start=start, stop=stop)
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(data, expected, rtol=1e-07, atol=0.0)
```

### Step 13: Assign ch_md = value

```python
ch_md = ts_channels[ch_name]['section_2']
```

### Step 14: Assign unknown = _get_mef_units_scale(...)

```python
scale, _, _, _, _ = _get_mef_units_scale(ch_md['units_description'], ch_md['units_conversion_factor'])
```

### Step 15: Call scales.append()

```python
scales.append(scale)
```


## Complete Example

```python
# Workflow
'Test that MNE scaling matches pymef data plus metadata scaling.'
raw = read_raw_mef(mef_file_path, preload=False)
session = pymef.mef_session.MefSession(str(mef_file_path), '')
ts_channels = session.session_md['time_series_channels']
scales = []
for ch_name in raw.ch_names:
    ch_md = ts_channels[ch_name]['section_2']
    scale, _, _, _, _ = _get_mef_units_scale(ch_md['units_description'], ch_md['units_conversion_factor'])
    scales.append(scale)
scales = np.array(scales)
assert not np.allclose(scales, 1)
start, stop = (0, 10)
pymef_data = session.read_ts_channels_sample(raw.ch_names, [start, stop])
pymef_data = np.array(pymef_data, dtype=np.float64)
expected = pymef_data * scales[:, np.newaxis]
data = raw.get_data(start=start, stop=stop)
np.testing.assert_allclose(data, expected, rtol=1e-07, atol=0.0)
```

## Next Steps


---

*Source: test_mef.py:171 | Complexity: Advanced | Last updated: 2026-05-18*