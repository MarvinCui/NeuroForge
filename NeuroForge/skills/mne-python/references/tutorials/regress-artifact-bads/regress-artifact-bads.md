# How To: Regress Artifact Bads

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that bad channels are handled properly.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`


## Step-by-Step Guide

### Step 1: 'Test that bad channels are handled properly.'

```python
'Test that bad channels are handled properly.'
```

**Verification:**
```python
assert len(raw.ch_names) == 13
```

### Step 2: Assign raw = read_raw_fif.del_proj.set_eeg_reference(...)

```python
raw = read_raw_fif(raw_fname).del_proj().set_eeg_reference(projection=True)
```

**Verification:**
```python
assert_array_equal(picks, np.arange(4, 12))
```

### Step 3: Assign picks_all = np.concatenate(...)

```python
picks_all = np.concatenate([pick_types(raw.info, meg=True)[:4], pick_types(raw.info, eeg=True)[:8], pick_types(raw.info, eog=True)[:1]])
```

**Verification:**
```python
assert_allclose(raw_reg.get_data('meg'), raw.get_data('meg'))
```

### Step 4: Call raw.pick.load_data()

```python
raw.pick(picks_all).load_data()
```

**Verification:**
```python
assert_array_less(3, suppression)
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, eeg=True)
```

**Verification:**
```python
assert_allclose(data_reg, data_reg_new)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(picks, np.arange(4, 12))
```

### Step 7: Assign norms = np.linalg.norm(...)

```python
norms = np.linalg.norm(raw.get_data(picks), axis=1)
```

### Step 8: Assign unknown = regress_artifact(...)

```python
raw_reg, _ = regress_artifact(raw, picks=picks, picks_artifact='eog')
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw_reg.get_data('meg'), raw.get_data('meg'))
```

### Step 10: Assign data_reg = raw_reg.get_data(...)

```python
data_reg = raw_reg.get_data()
```

### Step 11: Assign norms_reg = np.linalg.norm(...)

```python
norms_reg = np.linalg.norm(data_reg[picks], axis=1)
```

### Step 12: Assign suppression = value

```python
suppression = 20 * np.log10(norms / norms_reg)
```

### Step 13: Call assert_array_less()

```python
assert_array_less(3, suppression)
```

### Step 14: Assign unknown = value

```python
raw.info['bads'] = raw.ch_names[:2] + raw.ch_names[-2:-1]
```

### Step 15: Assign unknown = regress_artifact(...)

```python
raw_reg, _ = regress_artifact(raw, picks=picks, picks_artifact='eog')
```

### Step 16: Assign data_reg_new = raw_reg.get_data(...)

```python
data_reg_new = raw_reg.get_data()
```

### Step 17: Call assert_allclose()

```python
assert_allclose(data_reg, data_reg_new)
```


## Complete Example

```python
# Workflow
'Test that bad channels are handled properly.'
raw = read_raw_fif(raw_fname).del_proj().set_eeg_reference(projection=True)
picks_all = np.concatenate([pick_types(raw.info, meg=True)[:4], pick_types(raw.info, eeg=True)[:8], pick_types(raw.info, eog=True)[:1]])
raw.pick(picks_all).load_data()
assert len(raw.ch_names) == 13
del picks_all
picks = pick_types(raw.info, eeg=True)
assert_array_equal(picks, np.arange(4, 12))
norms = np.linalg.norm(raw.get_data(picks), axis=1)
raw_reg, _ = regress_artifact(raw, picks=picks, picks_artifact='eog')
assert_allclose(raw_reg.get_data('meg'), raw.get_data('meg'))
data_reg = raw_reg.get_data()
norms_reg = np.linalg.norm(data_reg[picks], axis=1)
suppression = 20 * np.log10(norms / norms_reg)
assert_array_less(3, suppression)
raw.info['bads'] = raw.ch_names[:2] + raw.ch_names[-2:-1]
raw_reg, _ = regress_artifact(raw, picks=picks, picks_artifact='eog')
data_reg_new = raw_reg.get_data()
assert_allclose(data_reg, data_reg_new)
```

## Next Steps


---

*Source: test_regress.py:156 | Complexity: Advanced | Last updated: 2026-05-18*