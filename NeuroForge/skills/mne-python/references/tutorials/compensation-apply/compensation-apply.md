# How To: Compensation Apply

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test applying compensation.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, preload, pick
```

## Step-by-Step Guide

### Step 1: 'Test applying compensation.'

```python
'Test applying compensation.'
```

**Verification:**
```python
assert raw._comp is None
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(ctf_comp_fname, preload=preload)
```

**Verification:**
```python
assert get_current_comp(raw2.info) == 2
```

### Step 3: Assign raw2 = raw.copy(...)

```python
raw2 = raw.copy()
```

**Verification:**
```python
assert raw2._comp is None
```

### Step 4: Call raw2.apply_gradient_compensation()

```python
raw2.apply_gradient_compensation(2)
```

**Verification:**
```python
assert raw2._comp.shape == (len(raw2.ch_names),) * 2
```

### Step 5: Assign fname = value

```python
fname = tmp_path / 'ctf-raw.fif'
```

**Verification:**
```python
assert raw2.compensation_grade == 2
```

### Step 6: Call raw2.save()

```python
raw2.save(fname)
```

**Verification:**
```python
assert raw2.compensation_grade == 3
```

### Step 7: Assign raw2 = read_raw_fif(...)

```python
raw2 = read_raw_fif(fname)
```

**Verification:**
```python
assert_allclose(data, data2, rtol=1e-09, atol=1e-18)
```

### Step 8: Call raw2.apply_gradient_compensation()

```python
raw2.apply_gradient_compensation(3)
```

**Verification:**
```python
assert ch1['coil_type'] == ch2['coil_type']
```

### Step 9: Assign unknown = value

```python
data, _ = raw[:, :]
```

### Step 10: Assign unknown = value

```python
data2, _ = raw2[:, :]
```

### Step 11: Call assert_allclose()

```python
assert_allclose(data, data2, rtol=1e-09, atol=1e-18)
```

### Step 12: Call raw2.pick()

```python
raw2.pick([0] + list(range(2, len(raw.ch_names))))
```

### Step 13: Call raw.pick()

```python
raw.pick([0] + list(range(2, len(raw.ch_names))))
```

**Verification:**
```python
assert raw2._comp is None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, preload, pick

# Workflow
'Test applying compensation.'
raw = read_raw_fif(ctf_comp_fname, preload=preload)
assert raw._comp is None
raw2 = raw.copy()
raw2.apply_gradient_compensation(2)
if pick:
    raw2.pick([0] + list(range(2, len(raw.ch_names))))
    raw.pick([0] + list(range(2, len(raw.ch_names))))
assert get_current_comp(raw2.info) == 2
if preload:
    assert raw2._comp is None
else:
    assert raw2._comp.shape == (len(raw2.ch_names),) * 2
fname = tmp_path / 'ctf-raw.fif'
raw2.save(fname)
raw2 = read_raw_fif(fname)
assert raw2.compensation_grade == 2
raw2.apply_gradient_compensation(3)
assert raw2.compensation_grade == 3
data, _ = raw[:, :]
data2, _ = raw2[:, :]
assert_allclose(data, data2, rtol=1e-09, atol=1e-18)
for ch1, ch2 in zip(raw.info['chs'], raw2.info['chs']):
    assert ch1['coil_type'] == ch2['coil_type']
```

## Next Steps


---

*Source: test_compensator.py:45 | Complexity: Advanced | Last updated: 2026-05-18*