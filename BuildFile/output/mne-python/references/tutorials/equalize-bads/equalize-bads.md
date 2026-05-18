# How To: Equalize Bads

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test equalize_bads function.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.preprocessing`
- `mne.preprocessing.interpolate`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: interp_thresh, inst_type
```

## Step-by-Step Guide

### Step 1: 'Test equalize_bads function.'

```python
'Test equalize_bads function.'
```

**Verification:**
```python
assert set(inst.info['bads']) == set(bads_ok)
```

### Step 2: Assign unknown = _load_data(...)

```python
raw, epochs, evoked = _load_data()
```

### Step 3: Assign bads = value

```python
bads = insts[0].copy().pick('eeg').ch_names[:3]
```

### Step 4: Assign unknown = value

```python
insts[0].info['bads'] = bads[:2]
```

### Step 5: Assign unknown = value

```python
insts[1].info['bads'] = bads[1:]
```

### Step 6: Assign insts_ok = equalize_bads(...)

```python
insts_ok = equalize_bads(insts, interp_thresh=interp_thresh)
```

### Step 7: Assign insts = value

```python
insts = [raw.copy().crop(0, 1), raw.copy().crop(0, 2)]
```

### Step 8: Call equalize_bads()

```python
equalize_bads(insts, interp_thresh=2.0)
```

### Step 9: Assign bads_ok = value

```python
bads_ok = []
```

**Verification:**
```python
assert set(inst.info['bads']) == set(bads_ok)
```

### Step 10: Assign insts = value

```python
insts = [epochs.copy()[:1], epochs.copy()[:2]]
```

### Step 11: Assign insts = value

```python
insts = [evoked.copy().crop(0, 0.1), raw.copy().crop(0, 0.2)]
```

### Step 12: Assign bads_ok = bads

```python
bads_ok = bads
```

### Step 13: Assign bads_ok = value

```python
bads_ok = bads[1:]
```


## Complete Example

```python
# Setup
# Fixtures: interp_thresh, inst_type

# Workflow
'Test equalize_bads function.'
raw, epochs, evoked = _load_data()
if inst_type == 'raw':
    insts = [raw.copy().crop(0, 1), raw.copy().crop(0, 2)]
elif inst_type == 'epochs':
    insts = [epochs.copy()[:1], epochs.copy()[:2]]
else:
    insts = [evoked.copy().crop(0, 0.1), raw.copy().crop(0, 0.2)]
with pytest.raises(ValueError, match='between 0'):
    equalize_bads(insts, interp_thresh=2.0)
bads = insts[0].copy().pick('eeg').ch_names[:3]
insts[0].info['bads'] = bads[:2]
insts[1].info['bads'] = bads[1:]
insts_ok = equalize_bads(insts, interp_thresh=interp_thresh)
if interp_thresh == 0:
    bads_ok = []
elif interp_thresh == 1:
    bads_ok = bads
else:
    bads_ok = bads[1:]
for inst in insts_ok:
    assert set(inst.info['bads']) == set(bads_ok)
```

## Next Steps


---

*Source: test_interpolate.py:49 | Complexity: Advanced | Last updated: 2026-05-18*