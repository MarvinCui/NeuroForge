# How To: Beer Lambert

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test converting raw CW amplitude files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.preprocessing.nirs._beer_lambert_law`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, fmt, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test converting raw CW amplitude files.'

```python
'Test converting raw CW amplitude files.'
```

**Verification:**
```python
assert len(raw_volt.ch_names) % nfreqs == 0
```

### Step 2: Assign raw_od = optical_density(...)

```python
raw_od = optical_density(raw_volt)
```

**Verification:**
```python
assert len(raw_hb.ch_names) % npairs == 0
```

### Step 3: Call _validate_type()

```python
_validate_type(raw_od, BaseRaw, 'raw')
```

**Verification:**
```python
assert len(raw_hb.ch_names) // npairs == 2.0
```

### Step 4: Assign raw_hb = beer_lambert_law(...)

```python
raw_hb = beer_lambert_law(raw_od)
```

**Verification:**
```python
assert set(raw_volt.get_channel_types()) == {'fnirs_cw_amplitude'}
```

### Step 5: Call _validate_type()

```python
_validate_type(raw_hb, BaseRaw, 'raw')
```

**Verification:**
```python
assert set(raw_hb.get_channel_types()) == {'hbo', 'hbr'}
```

### Step 6: Assign nfreqs = len(...)

```python
nfreqs = len(set(_channel_frequencies(raw_volt.info)))
```

**Verification:**
```python
assert old_prefixes == new_prefixes
```

### Step 7: Assign npairs = value

```python
npairs = len(raw_volt.ch_names) // nfreqs
```

**Verification:**
```python
assert all([name.split(' ')[1] in {'hbo', 'hbr'} for name in raw_hb.ch_names])
```

### Step 8: Assign old_prefixes = value

```python
old_prefixes = [name.split(' ')[0] for name in raw_volt.ch_names[::nfreqs]]
```

### Step 9: Assign new_prefixes = value

```python
new_prefixes = [name.split(' ')[0] for name in raw_hb.ch_names[::2]]
```

**Verification:**
```python
assert old_prefixes == new_prefixes
```

### Step 10: Call pytest.importorskip()

```python
pytest.importorskip('h5py')
```

### Step 11: Assign raw_volt = read_raw_nirx(...)

```python
raw_volt = read_raw_nirx(fname)
```

### Step 12: Assign raw_nirx = read_raw_nirx(...)

```python
raw_nirx = read_raw_nirx(fname)
```

### Step 13: Call raw_nirx.save()

```python
raw_nirx.save(tmp_path / 'test_raw.fif')
```

### Step 14: Assign raw_volt = read_raw_fif(...)

```python
raw_volt = read_raw_fif(tmp_path / 'test_raw.fif')
```

### Step 15: Assign raw_volt = read_raw_snirf(...)

```python
raw_volt = read_raw_snirf(fname)
```


## Complete Example

```python
# Setup
# Fixtures: fname, fmt, tmp_path

# Workflow
'Test converting raw CW amplitude files.'
if fname.suffix == '.snirf':
    pytest.importorskip('h5py')
match fmt:
    case 'nirx':
        raw_volt = read_raw_nirx(fname)
    case 'fif':
        raw_nirx = read_raw_nirx(fname)
        raw_nirx.save(tmp_path / 'test_raw.fif')
        raw_volt = read_raw_fif(tmp_path / 'test_raw.fif')
    case 'snirf':
        raw_volt = read_raw_snirf(fname)
    case _:
        raise ValueError(f"fmt expected to be one of 'nirx', 'fif' or 'snirf', got {fmt}")
raw_od = optical_density(raw_volt)
_validate_type(raw_od, BaseRaw, 'raw')
raw_hb = beer_lambert_law(raw_od)
_validate_type(raw_hb, BaseRaw, 'raw')
nfreqs = len(set(_channel_frequencies(raw_volt.info)))
assert len(raw_volt.ch_names) % nfreqs == 0
npairs = len(raw_volt.ch_names) // nfreqs
assert len(raw_hb.ch_names) % npairs == 0
assert len(raw_hb.ch_names) // npairs == 2.0
assert set(raw_volt.get_channel_types()) == {'fnirs_cw_amplitude'}
assert set(raw_hb.get_channel_types()) == {'hbo', 'hbr'}
old_prefixes = [name.split(' ')[0] for name in raw_volt.ch_names[::nfreqs]]
new_prefixes = [name.split(' ')[0] for name in raw_hb.ch_names[::2]]
assert old_prefixes == new_prefixes
assert all([name.split(' ')[1] in {'hbo', 'hbr'} for name in raw_hb.ch_names])
```

## Next Steps


---

*Source: test_beer_lambert_law.py:49 | Complexity: Advanced | Last updated: 2026-05-18*