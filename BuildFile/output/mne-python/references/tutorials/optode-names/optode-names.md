# How To: Optode Names

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Ensure optode name extraction is correct.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`


## Step-by-Step Guide

### Step 1: 'Ensure optode name extraction is correct.'

```python
'Ensure optode name extraction is correct.'
```

**Verification:**
```python
assert_array_equal(src_names, [f'S{n}' for n in ['2', '3', '11']])
```

### Step 2: Assign ch_names = value

```python
ch_names = ['S11_D2 760', 'S11_D2 850', 'S3_D1 760', 'S3_D1 850', 'S2_D13 760', 'S2_D13 850']
```

**Verification:**
```python
assert_array_equal(det_names, [f'D{n}' for n in ['1', '2', '13']])
```

### Step 3: Assign ch_types = np.repeat(...)

```python
ch_types = np.repeat('fnirs_od', 6)
```

**Verification:**
```python
assert_array_equal(src_names, [f'S{n}' for n in range(1, 4)])
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

**Verification:**
```python
assert_array_equal(det_names, [f'D{n}' for n in ['1', '11', '17']])
```

### Step 5: Assign unknown = _fnirs_optode_names(...)

```python
src_names, det_names = _fnirs_optode_names(info)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(src_names, [f'S{n}' for n in ['2', '3', '11']])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(det_names, [f'D{n}' for n in ['1', '2', '13']])
```

### Step 8: Assign ch_names = value

```python
ch_names = ['S1_D11 hbo', 'S1_D11 hbr', 'S2_D17 hbo', 'S2_D17 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
```

### Step 9: Assign ch_types = np.tile(...)

```python
ch_types = np.tile(['hbo', 'hbr'], 3)
```

### Step 10: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 11: Assign unknown = _fnirs_optode_names(...)

```python
src_names, det_names = _fnirs_optode_names(info)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(src_names, [f'S{n}' for n in range(1, 4)])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(det_names, [f'D{n}' for n in ['1', '11', '17']])
```


## Complete Example

```python
# Workflow
'Ensure optode name extraction is correct.'
ch_names = ['S11_D2 760', 'S11_D2 850', 'S3_D1 760', 'S3_D1 850', 'S2_D13 760', 'S2_D13 850']
ch_types = np.repeat('fnirs_od', 6)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
src_names, det_names = _fnirs_optode_names(info)
assert_array_equal(src_names, [f'S{n}' for n in ['2', '3', '11']])
assert_array_equal(det_names, [f'D{n}' for n in ['1', '2', '13']])
ch_names = ['S1_D11 hbo', 'S1_D11 hbr', 'S2_D17 hbo', 'S2_D17 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
src_names, det_names = _fnirs_optode_names(info)
assert_array_equal(src_names, [f'S{n}' for n in range(1, 4)])
assert_array_equal(det_names, [f'D{n}' for n in ['1', '11', '17']])
```

## Next Steps


---

*Source: test_nirs.py:511 | Complexity: Advanced | Last updated: 2026-05-18*