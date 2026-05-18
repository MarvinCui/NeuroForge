# How To: Read Dig Montage Using Polhemus Fastscan

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test FastScan.

## Prerequisites

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`


## Step-by-Step Guide

### Step 1: 'Test FastScan.'

```python
'Test FastScan.'
```

**Verification:**
```python
assert repr(montage) == '<DigMontage | 500 extras (headshape), 5 HPIs, 3 fiducials, 10 channels>'
```

### Step 2: Assign N_EEG_CH = 10

```python
N_EEG_CH = 10
```

**Verification:**
```python
assert set([d['coord_frame'] for d in montage.dig]) == {FIFF.FIFFV_COORD_UNKNOWN}
```

### Step 3: Assign my_electrode_positions = read_polhemus_fastscan(...)

```python
my_electrode_positions = read_polhemus_fastscan(kit_dir / 'test_elp.txt')
```

**Verification:**
```python
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
```

### Step 4: Assign montage = make_dig_montage(...)

```python
montage = make_dig_montage(ch_pos=dict(zip(ascii_lowercase[:N_EEG_CH], np.random.RandomState(0).rand(N_EEG_CH, 3))), nasion=my_electrode_positions[0], lpa=my_electrode_positions[1], rpa=my_electrode_positions[2], hpi=my_electrode_positions[3:], hsp=read_polhemus_fastscan(kit_dir / 'test_hsp.txt'), coord_frame='unknown')
```

**Verification:**
```python
assert_allclose(val, EXPECTED_FID_IN_POLHEMUS[kk])
```

### Step 5: Assign EXPECTED_FID_IN_POLHEMUS = value

```python
EXPECTED_FID_IN_POLHEMUS = {'nasion': [0.001393, 0.0131613, -0.0046967], 'lpa': [-0.0624997, -0.0737271, 0.07996], 'rpa': [-0.0748957, 0.0873785, 0.0811943]}
```

### Step 6: Assign unknown = _get_fid_coords(...)

```python
fiducials, fid_coordframe = _get_fid_coords(montage.dig)
```

**Verification:**
```python
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
```

### Step 7: Call assert_allclose()

```python
assert_allclose(val, EXPECTED_FID_IN_POLHEMUS[kk])
```


## Complete Example

```python
# Workflow
'Test FastScan.'
N_EEG_CH = 10
my_electrode_positions = read_polhemus_fastscan(kit_dir / 'test_elp.txt')
montage = make_dig_montage(ch_pos=dict(zip(ascii_lowercase[:N_EEG_CH], np.random.RandomState(0).rand(N_EEG_CH, 3))), nasion=my_electrode_positions[0], lpa=my_electrode_positions[1], rpa=my_electrode_positions[2], hpi=my_electrode_positions[3:], hsp=read_polhemus_fastscan(kit_dir / 'test_hsp.txt'), coord_frame='unknown')
assert repr(montage) == '<DigMontage | 500 extras (headshape), 5 HPIs, 3 fiducials, 10 channels>'
assert set([d['coord_frame'] for d in montage.dig]) == {FIFF.FIFFV_COORD_UNKNOWN}
EXPECTED_FID_IN_POLHEMUS = {'nasion': [0.001393, 0.0131613, -0.0046967], 'lpa': [-0.0624997, -0.0737271, 0.07996], 'rpa': [-0.0748957, 0.0873785, 0.0811943]}
fiducials, fid_coordframe = _get_fid_coords(montage.dig)
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
for kk, val in fiducials.items():
    assert_allclose(val, EXPECTED_FID_IN_POLHEMUS[kk])
```

## Next Steps


---

*Source: test_montage.py:698 | Complexity: Intermediate | Last updated: 2026-05-18*