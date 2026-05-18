# How To: Helmet

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test loading helmet surfaces.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test loading helmet surfaces.'

```python
'Test loading helmet surfaces.'
```

**Verification:**
```python
assert name in log
```

### Step 2: Assign base_dir = value

```python
base_dir = Path(__file__).parents[1] / 'io'
```

**Verification:**
```python
assert_equal(len(helmet['rr']), n)
```

### Step 3: Assign fname_raw = value

```python
fname_raw = base_dir / 'tests' / 'data' / 'test_raw.fif'
```

**Verification:**
```python
assert_equal(len(helmet['rr']), len(helmet['nn']))
```

### Step 4: Assign fname_kit_raw = value

```python
fname_kit_raw = base_dir / 'kit' / 'tests' / 'data' / 'test_bin_raw.fif'
```

### Step 5: Assign fname_bti_raw = value

```python
fname_bti_raw = base_dir / 'bti' / 'tests' / 'data' / 'exported4D_linux_raw.fif'
```

### Step 6: Assign fname_ctf_raw = value

```python
fname_ctf_raw = base_dir / 'tests' / 'data' / 'test_ctf_raw.fif'
```

### Step 7: Assign fname_trans = value

```python
fname_trans = base_dir / 'tests' / 'data' / 'sample-audvis-raw-trans.txt'
```

### Step 8: Assign trans = value

```python
trans = _get_trans(fname_trans)[0]
```

### Step 9: Assign new_info = read_info(...)

```python
new_info = read_info(fname_raw)
```

### Step 10: Assign artemis_info = new_info.copy(...)

```python
artemis_info = new_info.copy()
```

### Step 11: Assign unknown = 9999

```python
new_info['chs'][pick]['coil_type'] = 9999
```

### Step 12: Assign unknown = value

```python
artemis_info['chs'][pick]['coil_type'] = FIFF.FIFFV_COIL_ARTEMIS123_GRAD
```

### Step 13: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert name in log
```

### Step 14: Call assert_equal()

```python
assert_equal(len(helmet['rr']), n)
```

### Step 15: Call assert_equal()

```python
assert_equal(len(helmet['rr']), len(helmet['nn']))
```

### Step 16: Assign helmet = get_meg_helmet_surf(...)

```python
helmet = get_meg_helmet_surf(info, trans, verbose=True)
```


## Complete Example

```python
# Workflow
'Test loading helmet surfaces.'
base_dir = Path(__file__).parents[1] / 'io'
fname_raw = base_dir / 'tests' / 'data' / 'test_raw.fif'
fname_kit_raw = base_dir / 'kit' / 'tests' / 'data' / 'test_bin_raw.fif'
fname_bti_raw = base_dir / 'bti' / 'tests' / 'data' / 'exported4D_linux_raw.fif'
fname_ctf_raw = base_dir / 'tests' / 'data' / 'test_ctf_raw.fif'
fname_trans = base_dir / 'tests' / 'data' / 'sample-audvis-raw-trans.txt'
trans = _get_trans(fname_trans)[0]
new_info = read_info(fname_raw)
artemis_info = new_info.copy()
for pick in pick_types(new_info, meg=True):
    new_info['chs'][pick]['coil_type'] = 9999
    artemis_info['chs'][pick]['coil_type'] = FIFF.FIFFV_COIL_ARTEMIS123_GRAD
for info, n, name in [(read_info(fname_raw), 304, '306m'), (read_info(fname_kit_raw), 150, 'KIT'), (read_info(fname_bti_raw), 304, 'Magnes'), (read_info(fname_ctf_raw), 342, 'CTF'), (new_info, 102, 'unknown'), (artemis_info, 102, 'ARTEMIS123')]:
    with catch_logging() as log:
        helmet = get_meg_helmet_surf(info, trans, verbose=True)
    log = log.getvalue()
    assert name in log
    assert_equal(len(helmet['rr']), n)
    assert_equal(len(helmet['rr']), len(helmet['nn']))
```

## Next Steps


---

*Source: test_surface.py:49 | Complexity: Advanced | Last updated: 2026-05-18*