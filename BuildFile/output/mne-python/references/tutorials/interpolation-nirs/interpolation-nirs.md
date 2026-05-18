# How To: Interpolation Nirs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test interpolating bad nirs channels.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test interpolating bad nirs channels.'

```python
'Test interpolating bad nirs channels.'
```

**Verification:**
```python
assert raw_od.info['bads'] == bads_init[:2]
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pymatreader')
```

**Verification:**
```python
assert raw_od.info['bads'] == []
```

### Step 3: Assign fname = value

```python
fname = testing_path / 'NIRx' / 'nirscout' / 'nirx_15_2_recording_w_overlap'
```

**Verification:**
```python
assert bad_0_std_pre_interp > np.std(raw_od._data[bad_0])
```

### Step 4: Assign raw_intensity = read_raw_nirx(...)

```python
raw_intensity = read_raw_nirx(fname, preload=False)
```

**Verification:**
```python
assert raw_haemo.info['bads'] == ['S1_D2 hbo', 'S1_D2 hbr']
```

### Step 5: Assign raw_od = optical_density(...)

```python
raw_od = optical_density(raw_intensity)
```

**Verification:**
```python
assert raw_haemo.info['bads'] == []
```

### Step 6: Assign sci = scalp_coupling_index(...)

```python
sci = scalp_coupling_index(raw_od)
```

### Step 7: Assign unknown = list(...)

```python
raw_od.info['bads'] = list(compress(raw_od.ch_names, sci < 0.5))
```

### Step 8: Assign bad_0 = value

```python
bad_0 = np.where([name == raw_od.info['bads'][0] for name in raw_od.ch_names])[0][0]
```

### Step 9: Assign bad_0_std_pre_interp = np.std(...)

```python
bad_0_std_pre_interp = np.std(raw_od._data[bad_0])
```

### Step 10: Assign bads_init = list(...)

```python
bads_init = list(raw_od.info['bads'])
```

### Step 11: Call raw_od.interpolate_bads()

```python
raw_od.interpolate_bads(exclude=bads_init[:2])
```

**Verification:**
```python
assert raw_od.info['bads'] == bads_init[:2]
```

### Step 12: Call raw_od.interpolate_bads()

```python
raw_od.interpolate_bads()
```

**Verification:**
```python
assert raw_od.info['bads'] == []
```

### Step 13: Assign raw_haemo = beer_lambert_law(...)

```python
raw_haemo = beer_lambert_law(raw_od, ppf=6)
```

### Step 14: Assign unknown = value

```python
raw_haemo.info['bads'] = raw_haemo.ch_names[2:4]
```

**Verification:**
```python
assert raw_haemo.info['bads'] == ['S1_D2 hbo', 'S1_D2 hbr']
```

### Step 15: Call raw_haemo.interpolate_bads()

```python
raw_haemo.interpolate_bads()
```

**Verification:**
```python
assert raw_haemo.info['bads'] == []
```


## Complete Example

```python
# Workflow
'Test interpolating bad nirs channels.'
pytest.importorskip('pymatreader')
fname = testing_path / 'NIRx' / 'nirscout' / 'nirx_15_2_recording_w_overlap'
raw_intensity = read_raw_nirx(fname, preload=False)
raw_od = optical_density(raw_intensity)
sci = scalp_coupling_index(raw_od)
raw_od.info['bads'] = list(compress(raw_od.ch_names, sci < 0.5))
bad_0 = np.where([name == raw_od.info['bads'][0] for name in raw_od.ch_names])[0][0]
bad_0_std_pre_interp = np.std(raw_od._data[bad_0])
bads_init = list(raw_od.info['bads'])
raw_od.interpolate_bads(exclude=bads_init[:2])
assert raw_od.info['bads'] == bads_init[:2]
raw_od.interpolate_bads()
assert raw_od.info['bads'] == []
assert bad_0_std_pre_interp > np.std(raw_od._data[bad_0])
raw_haemo = beer_lambert_law(raw_od, ppf=6)
raw_haemo.info['bads'] = raw_haemo.ch_names[2:4]
assert raw_haemo.info['bads'] == ['S1_D2 hbo', 'S1_D2 hbr']
raw_haemo.interpolate_bads()
assert raw_haemo.info['bads'] == []
```

## Next Steps


---

*Source: test_interpolation.py:313 | Complexity: Advanced | Last updated: 2026-05-18*