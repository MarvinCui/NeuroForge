# How To: Set Standard Montage Mff

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test setting a standard montage.

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
# Fixtures: fname, standard_montage
```

## Step-by-Step Guide

### Step 1: 'Test setting a standard montage.'

```python
'Test setting a standard montage.'
```

**Verification:**
```python
assert len(dig_before_mon) == n_dig
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('defusedxml')
```

**Verification:**
```python
assert len(picks) == n_eeg
```

### Step 3: Assign raw = read_raw_egi(...)

```python
raw = read_raw_egi(fname, verbose='warning')
```

**Verification:**
```python
assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
```

### Step 4: Assign n_eeg = int(...)

```python
n_eeg = int(standard_montage.split('-')[-1])
```

**Verification:**
```python
assert len(dig_before_mon) == n_dig
```

### Step 5: Assign n_dig = value

```python
n_dig = n_eeg + 3
```

**Verification:**
```python
assert len(dig_after_mon) == n_dig
```

### Step 6: Assign dig_before_mon = deepcopy(...)

```python
dig_before_mon = deepcopy(raw.info['dig'])
```

**Verification:**
```python
assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
```

### Step 7: Assign ref_loc = value

```python
ref_loc = dig_before_mon[-1]['r']
```

### Step 8: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, eeg=True)
```

**Verification:**
```python
assert len(picks) == n_eeg
```

### Step 9: Call raw.set_montage()

```python
raw.set_montage(standard_montage, match_alias=True, on_missing='ignore')
```

### Step 10: Assign dig_after_mon = value

```python
dig_after_mon = raw.info['dig']
```

**Verification:**
```python
assert len(dig_before_mon) == n_dig
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
```


## Complete Example

```python
# Setup
# Fixtures: fname, standard_montage

# Workflow
'Test setting a standard montage.'
pytest.importorskip('defusedxml')
raw = read_raw_egi(fname, verbose='warning')
n_eeg = int(standard_montage.split('-')[-1])
n_dig = n_eeg + 3
dig_before_mon = deepcopy(raw.info['dig'])
assert len(dig_before_mon) == n_dig
ref_loc = dig_before_mon[-1]['r']
picks = pick_types(raw.info, eeg=True)
assert len(picks) == n_eeg
for pick in picks:
    assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
raw.set_montage(standard_montage, match_alias=True, on_missing='ignore')
dig_after_mon = raw.info['dig']
assert len(dig_before_mon) == n_dig
assert len(dig_after_mon) == n_dig
for pick in picks:
    assert_allclose(raw.info['chs'][pick]['loc'][3:6], ref_loc)
```

## Next Steps


---

*Source: test_egi.py:565 | Complexity: Advanced | Last updated: 2026-05-18*