# How To: Simulation Cascade

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that cascading operations do not overwrite data.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.chpi`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.simulation`
- `mne.simulation.source`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.tests.test_chpi`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that cascading operations do not overwrite data.'

```python
'Test that cascading operations do not overwrite data.'
```

**Verification:**
```python
assert_array_equal(raw_null.get_data(), 0.0)
```

### Step 2: Assign raw_null = read_raw_fif(...)

```python
raw_null = read_raw_fif(raw_chpi_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert_allclose(cascade_data, serial_data, atol=1e-20)
```

### Step 3: Call raw_null.crop.pick.load_data()

```python
raw_null.crop(0, 1).pick('meg').load_data()
```

### Step 4: Call raw_null.apply_function()

```python
raw_null.apply_function(lambda x: np.zeros_like(x))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(raw_null.get_data(), 0.0)
```

### Step 6: Assign raw_eog = raw_null.copy(...)

```python
raw_eog = raw_null.copy()
```

### Step 7: Call add_eog()

```python
add_eog(raw_eog, random_state=0)
```

### Step 8: Assign raw_ecg = raw_null.copy(...)

```python
raw_ecg = raw_null.copy()
```

### Step 9: Call add_ecg()

```python
add_ecg(raw_ecg, random_state=0)
```

### Step 10: Assign raw_noise = raw_null.copy(...)

```python
raw_noise = raw_null.copy()
```

### Step 11: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(raw_null.info)
```

### Step 12: Call add_noise()

```python
add_noise(raw_noise, cov, random_state=0)
```

### Step 13: Assign raw_chpi = raw_null.copy(...)

```python
raw_chpi = raw_null.copy()
```

### Step 14: Call add_chpi()

```python
add_chpi(raw_chpi)
```

### Step 15: Assign raw_cascade = raw_null.copy(...)

```python
raw_cascade = raw_null.copy()
```

### Step 16: Call add_eog()

```python
add_eog(raw_cascade, random_state=0)
```

### Step 17: Call add_ecg()

```python
add_ecg(raw_cascade, random_state=0)
```

### Step 18: Call add_chpi()

```python
add_chpi(raw_cascade)
```

### Step 19: Call add_noise()

```python
add_noise(raw_cascade, cov, random_state=0)
```

### Step 20: Assign cascade_data = raw_cascade.get_data(...)

```python
cascade_data = raw_cascade.get_data()
```

### Step 21: Assign serial_data = 0.0

```python
serial_data = 0.0
```

### Step 22: Call assert_allclose()

```python
assert_allclose(cascade_data, serial_data, atol=1e-20)
```


## Complete Example

```python
# Workflow
'Test that cascading operations do not overwrite data.'
raw_null = read_raw_fif(raw_chpi_fname, allow_maxshield='yes')
raw_null.crop(0, 1).pick('meg').load_data()
raw_null.apply_function(lambda x: np.zeros_like(x))
assert_array_equal(raw_null.get_data(), 0.0)
raw_eog = raw_null.copy()
add_eog(raw_eog, random_state=0)
raw_ecg = raw_null.copy()
add_ecg(raw_ecg, random_state=0)
raw_noise = raw_null.copy()
cov = make_ad_hoc_cov(raw_null.info)
add_noise(raw_noise, cov, random_state=0)
raw_chpi = raw_null.copy()
add_chpi(raw_chpi)
raw_cascade = raw_null.copy()
add_eog(raw_cascade, random_state=0)
add_ecg(raw_cascade, random_state=0)
add_chpi(raw_cascade)
add_noise(raw_cascade, cov, random_state=0)
cascade_data = raw_cascade.get_data()
serial_data = 0.0
for raw_other in (raw_eog, raw_ecg, raw_noise, raw_chpi):
    serial_data += raw_other.get_data()
assert_allclose(cascade_data, serial_data, atol=1e-20)
```

## Next Steps


---

*Source: test_raw.py:583 | Complexity: Advanced | Last updated: 2026-05-18*