# How To: Legendre Table

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Legendre table calculation.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.polynomial`
- `numpy.testing`
- `scipy.interpolate`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.forward._field_interpolation`
- `mne.forward._lead_dots`
- `mne.forward._make_forward`
- `mne.io`
- `mne.surface`


## Step-by-Step Guide

### Step 1: 'Test Legendre table calculation.'

```python
'Test Legendre table calculation.'
```

**Verification:**
```python
assert_allclose(lut1, lut2)
```

### Step 2: Assign n = 10

```python
n = 10
```

**Verification:**
```python
assert_allclose(n_fact1, n_fact2)
```

### Step 3: Assign unknown = _get_legen_table(...)

```python
lut1, n_fact1 = _get_legen_table(ch_type, n_coeff=25, force_calc=True)
```

### Step 4: Assign lut1 = unknown.copy(...)

```python
lut1 = lut1[:, :n - 1].copy()
```

### Step 5: Assign n_fact1 = unknown.copy(...)

```python
n_fact1 = n_fact1[:n - 1].copy()
```

### Step 6: Assign unknown = _get_legen_table(...)

```python
lut2, n_fact2 = _get_legen_table(ch_type, n_coeff=n, force_calc=True)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(lut1, lut2)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(n_fact1, n_fact2)
```


## Complete Example

```python
# Workflow
'Test Legendre table calculation.'
n = 10
for ch_type in ['eeg', 'meg']:
    lut1, n_fact1 = _get_legen_table(ch_type, n_coeff=25, force_calc=True)
    lut1 = lut1[:, :n - 1].copy()
    n_fact1 = n_fact1[:n - 1].copy()
    lut2, n_fact2 = _get_legen_table(ch_type, n_coeff=n, force_calc=True)
    assert_allclose(lut1, lut2)
    assert_allclose(n_fact1, n_fact2)
```

## Next Steps


---

*Source: test_field_interpolation.py:118 | Complexity: Advanced | Last updated: 2026-05-18*