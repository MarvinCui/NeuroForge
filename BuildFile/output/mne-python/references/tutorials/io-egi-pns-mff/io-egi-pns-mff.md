# How To: Io Egi Pns Mff

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test importing EGI MFF with PNS data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.egi.egi`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test importing EGI MFF with PNS data.'

```python
'Test importing EGI MFF with PNS data.'
```

**Verification:**
```python
assert 'RawMff' in repr(raw)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert len(pns_chans) == 7
```

### Step 3: Assign raw = read_raw_egi(...)

```python
raw = read_raw_egi(egi_mff_pns_fname, include=None, preload=True, verbose='error')
```

**Verification:**
```python
assert names == pns_names
```

### Step 4: Assign pns_chans = pick_types(...)

```python
pns_chans = pick_types(raw.info, ecg=True, bio=True, emg=True)
```

**Verification:**
```python
assert_array_equal(mat_data, raw_data)
```

### Step 5: Assign names = value

```python
names = [raw.ch_names[x] for x in pns_chans]
```

### Step 6: Assign pns_names = value

```python
pns_names = ['Resp. Temperature', 'Resp. Pressure', 'ECG', 'Body Position', 'Resp. Effort Chest', 'Resp. Effort Abdomen', 'EMG-Leg']
```

### Step 7: Call _test_raw_reader()

```python
_test_raw_reader(read_raw_egi, input_fname=egi_mff_pns_fname, channel_naming='EEG %03d', verbose='error', test_rank='less', test_scaling=False)
```

**Verification:**
```python
assert names == pns_names
```

### Step 8: Assign mat_names = value

```python
mat_names = ['Resp_Temperature', 'Resp_Pressure', 'ECG', 'Body_Position', 'Resp_Effort_Chest', 'Resp_Effort_Abdomen', 'EMGLeg']
```

### Step 9: Assign egi_fname_mat = value

```python
egi_fname_mat = testing_path / 'EGI' / 'test_egi_pns.mat'
```

### Step 10: Assign mc = sio.loadmat(...)

```python
mc = sio.loadmat(egi_fname_mat)
```

### Step 11: Assign new_mff = value

```python
new_mff = tmp_path / 'temp.mff'
```

### Step 12: Call copytree_rw()

```python
copytree_rw(egi_mff_pns_fname, new_mff)
```

### Step 13: Call read_raw_egi()

```python
read_raw_egi(new_mff, verbose='error')
```

### Step 14: Call os.remove()

```python
os.remove(new_mff / 'info1.xml')
```

### Step 15: Call os.remove()

```python
os.remove(new_mff / 'signal1.bin')
```

### Step 16: Call print()

```python
print(f'Testing {ch_name}')
```

### Step 17: Assign mc_key = value

```python
mc_key = [x for x in mc.keys() if mat_name in x][0]
```

### Step 18: Assign cal = value

```python
cal = raw.info['chs'][ch_idx]['cal']
```

### Step 19: Assign mat_data = value

```python
mat_data = mc[mc_key] * cal
```

### Step 20: Assign raw_data = value

```python
raw_data = raw[ch_idx][0]
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(mat_data, raw_data)
```

### Step 22: Call read_raw_egi()

```python
read_raw_egi(new_mff, verbose='error')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test importing EGI MFF with PNS data.'
pytest.importorskip('defusedxml')
raw = read_raw_egi(egi_mff_pns_fname, include=None, preload=True, verbose='error')
assert 'RawMff' in repr(raw)
pns_chans = pick_types(raw.info, ecg=True, bio=True, emg=True)
assert len(pns_chans) == 7
names = [raw.ch_names[x] for x in pns_chans]
pns_names = ['Resp. Temperature', 'Resp. Pressure', 'ECG', 'Body Position', 'Resp. Effort Chest', 'Resp. Effort Abdomen', 'EMG-Leg']
_test_raw_reader(read_raw_egi, input_fname=egi_mff_pns_fname, channel_naming='EEG %03d', verbose='error', test_rank='less', test_scaling=False)
assert names == pns_names
mat_names = ['Resp_Temperature', 'Resp_Pressure', 'ECG', 'Body_Position', 'Resp_Effort_Chest', 'Resp_Effort_Abdomen', 'EMGLeg']
egi_fname_mat = testing_path / 'EGI' / 'test_egi_pns.mat'
mc = sio.loadmat(egi_fname_mat)
for ch_name, ch_idx, mat_name in zip(pns_names, pns_chans, mat_names):
    print(f'Testing {ch_name}')
    mc_key = [x for x in mc.keys() if mat_name in x][0]
    cal = raw.info['chs'][ch_idx]['cal']
    mat_data = mc[mc_key] * cal
    raw_data = raw[ch_idx][0]
    assert_array_equal(mat_data, raw_data)
new_mff = tmp_path / 'temp.mff'
copytree_rw(egi_mff_pns_fname, new_mff)
read_raw_egi(new_mff, verbose='error')
os.remove(new_mff / 'info1.xml')
os.remove(new_mff / 'signal1.bin')
with pytest.raises(FileNotFoundError, match='Could not find any EEG'):
    read_raw_egi(new_mff, verbose='error')
```

## Next Steps


---

*Source: test_egi.py:292 | Complexity: Advanced | Last updated: 2026-05-18*