# How To: Ar Raw

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fitting AR model on raw data.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal`
- `mne`
- `mne.time_frequency.ar`
- `statsmodels.regression.linear_model`


## Step-by-Step Guide

### Step 1: 'Test fitting AR model on raw data.'

```python
'Test fitting AR model on raw data.'
```

**Verification:**
```python
assert coeffs.shape == (order,)
```

### Step 2: Assign raw = io.read_raw_fif.crop.load_data(...)

```python
raw = io.read_raw_fif(raw_fname).crop(0, 2).load_data()
```

**Verification:**
```python
assert_allclose(-coeffs[0], 1.0, atol=0.5)
```

### Step 3: Call raw.pick()

```python
raw.pick(picks='grad')
```

**Verification:**
```python
assert_allclose(coeffs, [1.0] + [0.0] * order, atol=0.02)
```

### Step 4: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(coeffs, iir + [0.0] * (order - 2), atol=0.05)
```

### Step 5: Assign raw._data = rng.randn(...)

```python
raw._data = rng.randn(*raw._data.shape)
```

### Step 6: Assign iir = value

```python
iir = [1, -1, 0.2]
```

### Step 7: Assign raw._data = lfilter(...)

```python
raw._data = lfilter([1.0], iir, raw._data)
```

### Step 8: Assign coeffs = value

```python
coeffs = fit_iir_model_raw(raw, order)[1][1:]
```

**Verification:**
```python
assert coeffs.shape == (order,)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(-coeffs[0], 1.0, atol=0.5)
```

### Step 10: Assign coeffs = value

```python
coeffs = fit_iir_model_raw(raw, order)[1]
```

### Step 11: Call assert_allclose()

```python
assert_allclose(coeffs, [1.0] + [0.0] * order, atol=0.02)
```

### Step 12: Assign coeffs = value

```python
coeffs = fit_iir_model_raw(raw, order)[1]
```

### Step 13: Call assert_allclose()

```python
assert_allclose(coeffs, iir + [0.0] * (order - 2), atol=0.05)
```


## Complete Example

```python
# Workflow
'Test fitting AR model on raw data.'
raw = io.read_raw_fif(raw_fname).crop(0, 2).load_data()
raw.pick(picks='grad')
for order in (2, 5, 10):
    coeffs = fit_iir_model_raw(raw, order)[1][1:]
    assert coeffs.shape == (order,)
    assert_allclose(-coeffs[0], 1.0, atol=0.5)
rng = np.random.RandomState(0)
raw._data = rng.randn(*raw._data.shape)
raw._data *= 1e-15
for order in (2, 5, 10):
    coeffs = fit_iir_model_raw(raw, order)[1]
    assert_allclose(coeffs, [1.0] + [0.0] * order, atol=0.02)
iir = [1, -1, 0.2]
raw._data = lfilter([1.0], iir, raw._data)
for order in (2, 5, 10):
    coeffs = fit_iir_model_raw(raw, order)[1]
    assert_allclose(coeffs, iir + [0.0] * (order - 2), atol=0.05)
```

## Next Steps


---

*Source: test_ar.py:31 | Complexity: Advanced | Last updated: 2026-05-18*