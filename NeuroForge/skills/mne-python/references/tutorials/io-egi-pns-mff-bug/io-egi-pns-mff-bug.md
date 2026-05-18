# How To: Io Egi Pns Mff Bug

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test importing EGI MFF with PNS data (BUG).

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
# Fixtures: preload
```

## Step-by-Step Guide

### Step 1: 'Test importing EGI MFF with PNS data (BUG).'

```python
'Test importing EGI MFF with PNS data (BUG).'
```

**Verification:**
```python
assert len(raw.annotations) == 1
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert_allclose(raw.annotations.duration, [0.004])
```

### Step 3: Assign egi_fname_mff = value

```python
egi_fname_mff = testing_path / 'EGI' / 'test_egi_pns_bug.mff'
```

**Verification:**
```python
assert_allclose(raw.annotations.onset, [13.948])
```

### Step 4: Call assert_allclose()

```python
assert_allclose(raw.annotations.duration, [0.004])
```

**Verification:**
```python
assert_array_equal(mat_data, raw_data)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(raw.annotations.onset, [13.948])
```

### Step 6: Assign egi_fname_mat = value

```python
egi_fname_mat = testing_path / 'EGI' / 'test_egi_pns.mat'
```

### Step 7: Assign mc = sio.loadmat(...)

```python
mc = sio.loadmat(egi_fname_mat)
```

### Step 8: Assign pns_chans = pick_types(...)

```python
pns_chans = pick_types(raw.info, ecg=True, bio=True, emg=True)
```

### Step 9: Assign pns_names = value

```python
pns_names = ['Resp. Temperature'[:15], 'Resp. Pressure', 'ECG', 'Body Position', 'Resp. Effort Chest'[:15], 'Resp. Effort Abdomen'[:15], 'EMG-Leg']
```

### Step 10: Assign mat_names = value

```python
mat_names = ['Resp_Temperature'[:15], 'Resp_Pressure', 'ECG', 'Body_Position', 'Resp_Effort_Chest'[:15], 'Resp_Effort_Abdomen'[:15], 'EMGLeg']
```

### Step 11: Assign raw = read_raw_egi(...)

```python
raw = read_raw_egi(egi_fname_mff, include=None, preload=preload, verbose='warning')
```

### Step 12: Call print()

```python
print(f'Testing {ch_name}')
```

### Step 13: Assign mc_key = value

```python
mc_key = [x for x in mc.keys() if mat_name in x][0]
```

### Step 14: Assign cal = value

```python
cal = raw.info['chs'][ch_idx]['cal']
```

### Step 15: Assign mat_data = value

```python
mat_data = mc[mc_key] * cal
```

### Step 16: Assign unknown = 0

```python
mat_data[:, -1] = 0
```

### Step 17: Assign raw_data = value

```python
raw_data = raw[ch_idx][0]
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(mat_data, raw_data)
```


## Complete Example

```python
# Setup
# Fixtures: preload

# Workflow
'Test importing EGI MFF with PNS data (BUG).'
pytest.importorskip('defusedxml')
egi_fname_mff = testing_path / 'EGI' / 'test_egi_pns_bug.mff'
with pytest.warns(RuntimeWarning, match='EGI PSG sample bug'):
    raw = read_raw_egi(egi_fname_mff, include=None, preload=preload, verbose='warning')
assert len(raw.annotations) == 1
assert_allclose(raw.annotations.duration, [0.004])
assert_allclose(raw.annotations.onset, [13.948])
egi_fname_mat = testing_path / 'EGI' / 'test_egi_pns.mat'
mc = sio.loadmat(egi_fname_mat)
pns_chans = pick_types(raw.info, ecg=True, bio=True, emg=True)
pns_names = ['Resp. Temperature'[:15], 'Resp. Pressure', 'ECG', 'Body Position', 'Resp. Effort Chest'[:15], 'Resp. Effort Abdomen'[:15], 'EMG-Leg']
mat_names = ['Resp_Temperature'[:15], 'Resp_Pressure', 'ECG', 'Body_Position', 'Resp_Effort_Chest'[:15], 'Resp_Effort_Abdomen'[:15], 'EMGLeg']
for ch_name, ch_idx, mat_name in zip(pns_names, pns_chans, mat_names):
    print(f'Testing {ch_name}')
    mc_key = [x for x in mc.keys() if mat_name in x][0]
    cal = raw.info['chs'][ch_idx]['cal']
    mat_data = mc[mc_key] * cal
    mat_data[:, -1] = 0
    raw_data = raw[ch_idx][0]
    assert_array_equal(mat_data, raw_data)
```

## Next Steps


---

*Source: test_egi.py:349 | Complexity: Advanced | Last updated: 2026-05-18*