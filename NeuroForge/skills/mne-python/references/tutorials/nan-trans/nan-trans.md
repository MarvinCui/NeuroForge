# How To: Nan Trans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test unlikely case that the device to head transform is empty.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `collections`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.bti.bti`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: pdf, config, hs, exported
```

## Step-by-Step Guide

### Step 1: 'Test unlikely case that the device to head transform is empty.'

```python
'Test unlikely case that the device to head transform is empty.'
```

### Step 2: Assign bti_info = _read_bti_header(...)

```python
bti_info = _read_bti_header(pdf, config, sort_by_ch_name=True)
```

### Step 3: Assign dev_ctf_t = Transform(...)

```python
dev_ctf_t = Transform('ctf_meg', 'ctf_head', _correct_trans(bti_info['bti_transform'][0]))
```

### Step 4: Assign convert = True

```python
convert = True
```

### Step 5: Assign rotation_x = 0.0

```python
rotation_x = 0.0
```

### Step 6: Assign translation = value

```python
translation = (0.0, 0.02, 0.11)
```

### Step 7: Assign bti_dev_t = _get_bti_dev_t(...)

```python
bti_dev_t = _get_bti_dev_t(rotation_x, translation)
```

### Step 8: Assign bti_dev_t = Transform(...)

```python
bti_dev_t = Transform('ctf_meg', 'meg', bti_dev_t)
```

### Step 9: Assign ecg_ch = 'E31'

```python
ecg_ch = 'E31'
```

### Step 10: Assign eog_ch = value

```python
eog_ch = ('E63', 'E64')
```

### Step 11: Assign bti_ch_names = list(...)

```python
bti_ch_names = list()
```

### Step 12: Assign neuromag_ch_names = _rename_channels(...)

```python
neuromag_ch_names = _rename_channels(bti_ch_names, ecg_ch=ecg_ch, eog_ch=eog_ch)
```

### Step 13: Assign ch_mapping = zip(...)

```python
ch_mapping = zip(bti_ch_names, neuromag_ch_names)
```

### Step 14: Assign unknown = value

```python
dev_ctf_t['trans'][:, 3] = np.nan
```

### Step 15: Call _check_nan_dev_head_t()

```python
_check_nan_dev_head_t(dev_ctf_t)
```

### Step 16: Assign ch_name = value

```python
ch_name = ch['name']
```

### Step 17: Call bti_ch_names.append()

```python
bti_ch_names.append(ch_name)
```

### Step 18: Assign loc = value

```python
loc = bti_info['chs'][idx]['loc']
```

### Step 19: Assign ch_name = ch.get(...)

```python
ch_name = ch.get('chan_label', ch_name)
```

### Step 20: Assign t = _loc_to_coil_trans(...)

```python
t = _loc_to_coil_trans(bti_info['chs'][idx]['loc'])
```

### Step 21: Assign t = _convert_coil_trans(...)

```python
t = _convert_coil_trans(t, dev_ctf_t, bti_dev_t)
```


## Complete Example

```python
# Setup
# Fixtures: pdf, config, hs, exported

# Workflow
'Test unlikely case that the device to head transform is empty.'
bti_info = _read_bti_header(pdf, config, sort_by_ch_name=True)
dev_ctf_t = Transform('ctf_meg', 'ctf_head', _correct_trans(bti_info['bti_transform'][0]))
convert = True
rotation_x = 0.0
translation = (0.0, 0.02, 0.11)
bti_dev_t = _get_bti_dev_t(rotation_x, translation)
bti_dev_t = Transform('ctf_meg', 'meg', bti_dev_t)
ecg_ch = 'E31'
eog_ch = ('E63', 'E64')
bti_ch_names = list()
for ch in bti_info['chs']:
    ch_name = ch['name']
    if not ch_name.startswith('A'):
        ch_name = ch.get('chan_label', ch_name)
    bti_ch_names.append(ch_name)
neuromag_ch_names = _rename_channels(bti_ch_names, ecg_ch=ecg_ch, eog_ch=eog_ch)
ch_mapping = zip(bti_ch_names, neuromag_ch_names)
dev_ctf_t['trans'][:, 3] = np.nan
_check_nan_dev_head_t(dev_ctf_t)
for idx, (chan_4d, chan_neuromag) in enumerate(ch_mapping):
    loc = bti_info['chs'][idx]['loc']
    if loc is not None:
        if convert:
            t = _loc_to_coil_trans(bti_info['chs'][idx]['loc'])
            t = _convert_coil_trans(t, dev_ctf_t, bti_dev_t)
```

## Next Steps


---

*Source: test_bti.py:388 | Complexity: Advanced | Last updated: 2026-05-18*