# How To: Plot Evoked Topomap Border

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test topomap extrapolation border values.

## Prerequisites

**Required Modules:**
- `functools`
- `pathlib`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.patches`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.time_frequency.tfr`
- `mne.viz`
- `mne.viz.tests.test_raw`
- `mne.viz.topomap`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test topomap extrapolation border values.'

```python
'Test topomap extrapolation border values.'
```

**Verification:**
```python
assert_equal(img_data[idx, idx], data[0])
```

### Step 2: Assign ch_pos = np.array.reshape(...)

```python
ch_pos = np.array([[[r, 0, 0], [-r, 0, 0], [0, r, 0], [0, -r, 0], [0, 0, r]] for r in np.linspace(0.2, 1, 5)]).reshape(-1, 3)
```

**Verification:**
```python
assert img_data[0, 0] < 1.5
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(len(ch_pos), 250, 'eeg')
```

**Verification:**
```python
assert_equal(img_data[idx, idx], data[0])
```

### Step 4: Assign ch_pos_dict = value

```python
ch_pos_dict = {name: pos for name, pos in zip(info['ch_names'], ch_pos)}
```

**Verification:**
```python
assert_almost_equal(img_data[idx, idx], data[0], decimal=9)
```

### Step 5: Assign dig = make_dig_montage(...)

```python
dig = make_dig_montage(ch_pos_dict, coord_frame='head')
```

### Step 6: Call info.set_montage()

```python
info.set_montage(dig)
```

### Step 7: Assign data = np.full(...)

```python
data = np.full(len(ch_pos), 5)
```

### Step 8: Assign kwargs = dict(...)

```python
kwargs = dict(res=15, extrapolate='head', sphere=1, sensors=False)
```

### Step 9: Assign idx = value

```python
idx = kwargs['res'] // 2
```

### Step 10: Assign unknown = plot_topomap(...)

```python
img, _ = plot_topomap(data, info, border=0, **kwargs)
```

### Step 11: Assign img_data = value

```python
img_data = img.get_array().data
```

### Step 12: Call assert_equal()

```python
assert_equal(img_data[idx, idx], data[0])
```

**Verification:**
```python
assert img_data[0, 0] < 1.5
```

### Step 13: Assign unknown = plot_topomap(...)

```python
img, _ = plot_topomap(data, info, border='mean', **kwargs)
```

### Step 14: Assign img_data = value

```python
img_data = img.get_array().data
```

### Step 15: Call assert_equal()

```python
assert_equal(img_data[idx, idx], data[0])
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(img_data[idx, idx], data[0], decimal=9)
```


## Complete Example

```python
# Workflow
'Test topomap extrapolation border values.'
ch_pos = np.array([[[r, 0, 0], [-r, 0, 0], [0, r, 0], [0, -r, 0], [0, 0, r]] for r in np.linspace(0.2, 1, 5)]).reshape(-1, 3)
info = create_info(len(ch_pos), 250, 'eeg')
ch_pos_dict = {name: pos for name, pos in zip(info['ch_names'], ch_pos)}
dig = make_dig_montage(ch_pos_dict, coord_frame='head')
info.set_montage(dig)
data = np.full(len(ch_pos), 5)
kwargs = dict(res=15, extrapolate='head', sphere=1, sensors=False)
idx = kwargs['res'] // 2
img, _ = plot_topomap(data, info, border=0, **kwargs)
img_data = img.get_array().data
assert_equal(img_data[idx, idx], data[0])
assert img_data[0, 0] < 1.5
img, _ = plot_topomap(data, info, border='mean', **kwargs)
img_data = img.get_array().data
assert_equal(img_data[idx, idx], data[0])
assert_almost_equal(img_data[idx, idx], data[0], decimal=9)
```

## Next Steps


---

*Source: test_topomap.py:296 | Complexity: Advanced | Last updated: 2026-05-18*