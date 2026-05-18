# How To: Make Dig Points

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test application of Polhemus HSP to info.

## Prerequisites

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`


## Step-by-Step Guide

### Step 1: 'Test application of Polhemus HSP to info.'

```python
'Test application of Polhemus HSP to info.'
```

**Verification:**
```python
assert info['dig'] is None
```

### Step 2: Assign extra_points = read_polhemus_fastscan(...)

```python
extra_points = read_polhemus_fastscan(hsp_fname, on_header_missing='ignore')
```

**Verification:**
```python
assert info['dig']
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names=['Test Ch'], sfreq=1000.0)
```

**Verification:**
```python
assert_allclose(info['dig'][0]['r'], [-0.10693, 0.0998, 0.06881])
```

### Step 4: Call assert_allclose()

```python
assert_allclose(info['dig'][0]['r'], [-0.10693, 0.0998, 0.06881])
```

**Verification:**
```python
assert info['dig'] is None
```

### Step 5: Assign elp_points = read_polhemus_fastscan(...)

```python
elp_points = read_polhemus_fastscan(elp_fname, on_header_missing='ignore')
```

**Verification:**
```python
assert info['dig']
```

### Step 6: Assign unknown = value

```python
nasion, lpa, rpa = elp_points[:3]
```

**Verification:**
```python
assert_allclose(info['dig'][idx]['r'], [0.001393, 0.0131613, -0.0046967])
```

### Step 7: Assign info = create_info(...)

```python
info = create_info(ch_names=['Test Ch'], sfreq=1000.0)
```

**Verification:**
```python
assert info['dig'] is None
```

### Step 8: Assign idx = unknown.index(...)

```python
idx = [d['ident'] for d in info['dig']].index(FIFF.FIFFV_POINT_NASION)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(info['dig'][idx]['r'], [0.001393, 0.0131613, -0.0046967])
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, _make_dig_points, nasion[:2])
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, _make_dig_points, None, lpa[:2])
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, _make_dig_points, None, None, rpa[:2])
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, _make_dig_points, None, None, None, elp_points[:, :2])
```

### Step 14: Call pytest.raises()

```python
pytest.raises(ValueError, _make_dig_points, None, None, None, None, elp_points[:, :2])
```

### Step 15: Assign unknown = _make_dig_points(...)

```python
info['dig'] = _make_dig_points(extra_points=extra_points)
```

### Step 16: Assign unknown = _make_dig_points(...)

```python
info['dig'] = _make_dig_points(nasion, lpa, rpa, elp_points[3:], None)
```


## Complete Example

```python
# Workflow
'Test application of Polhemus HSP to info.'
extra_points = read_polhemus_fastscan(hsp_fname, on_header_missing='ignore')
info = create_info(ch_names=['Test Ch'], sfreq=1000.0)
assert info['dig'] is None
with info._unlock():
    info['dig'] = _make_dig_points(extra_points=extra_points)
assert info['dig']
assert_allclose(info['dig'][0]['r'], [-0.10693, 0.0998, 0.06881])
elp_points = read_polhemus_fastscan(elp_fname, on_header_missing='ignore')
nasion, lpa, rpa = elp_points[:3]
info = create_info(ch_names=['Test Ch'], sfreq=1000.0)
assert info['dig'] is None
with info._unlock():
    info['dig'] = _make_dig_points(nasion, lpa, rpa, elp_points[3:], None)
assert info['dig']
idx = [d['ident'] for d in info['dig']].index(FIFF.FIFFV_POINT_NASION)
assert_allclose(info['dig'][idx]['r'], [0.001393, 0.0131613, -0.0046967])
pytest.raises(ValueError, _make_dig_points, nasion[:2])
pytest.raises(ValueError, _make_dig_points, None, lpa[:2])
pytest.raises(ValueError, _make_dig_points, None, None, rpa[:2])
pytest.raises(ValueError, _make_dig_points, None, None, None, elp_points[:, :2])
pytest.raises(ValueError, _make_dig_points, None, None, None, None, elp_points[:, :2])
```

## Next Steps


---

*Source: test_meas_info.py:518 | Complexity: Advanced | Last updated: 2026-05-18*