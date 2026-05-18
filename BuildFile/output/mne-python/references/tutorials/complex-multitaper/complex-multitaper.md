# How To: Complex Multitaper

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test complex-valued multitaper output.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.psd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test complex-valued multitaper output.'

```python
'Test complex-valued multitaper output.'
```

**Verification:**
```python
assert_array_equal(freq_complex, freq)
```

### Step 2: Assign unknown = _make_psd_data(...)

```python
data, sfreq, _ = _make_psd_data()
```

**Verification:**
```python
assert psd_complex.ndim == 3
```

### Step 3: Assign unknown = psd_array_multitaper(...)

```python
psd_complex, freq_complex, weights = psd_array_multitaper(data[:4, :500], sfreq, output='complex')
```

**Verification:**
```python
assert_allclose(psd_from_complex, psd)
```

### Step 4: Assign unknown = psd_array_multitaper(...)

```python
psd, freq = psd_array_multitaper(data[:4, :500], sfreq, output='power')
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(freq_complex, freq)
```

**Verification:**
```python
assert psd_complex.ndim == 3
```

### Step 6: Assign psd_from_complex = _psd_from_mt(...)

```python
psd_from_complex = _psd_from_mt(psd_complex, weights)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(psd_from_complex, psd)
```


## Complete Example

```python
# Workflow
'Test complex-valued multitaper output.'
data, sfreq, _ = _make_psd_data()
psd_complex, freq_complex, weights = psd_array_multitaper(data[:4, :500], sfreq, output='complex')
psd, freq = psd_array_multitaper(data[:4, :500], sfreq, output='power')
assert_array_equal(freq_complex, freq)
assert psd_complex.ndim == 3
psd_from_complex = _psd_from_mt(psd_complex, weights)
assert_allclose(psd_from_complex, psd)
```

## Next Steps


---

*Source: test_psd.py:129 | Complexity: Intermediate | Last updated: 2026-05-18*