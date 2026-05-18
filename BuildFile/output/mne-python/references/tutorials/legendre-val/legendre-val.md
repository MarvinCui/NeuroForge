# How To: Legendre Val

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Legendre polynomial (derivative) equivalence.

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

### Step 1: 'Test Legendre polynomial (derivative) equivalence.'

```python
'Test Legendre polynomial (derivative) equivalence.'
```

**Verification:**
```python
assert_allclose(vals_np[:, 1:vals_i.shape[1] + 1], vals_i, rtol=0.01, atol=0.005)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(c1, c2, 0.01, 0.001)
```

### Step 3: Assign xs = np.linspace(...)

```python
xs = np.linspace(-1.0, 1.0, 1000)
```

### Step 4: Assign n_terms = 100

```python
n_terms = 100
```

### Step 5: Assign vals_np = legendre.legvander(...)

```python
vals_np = legendre.legvander(xs, n_terms - 1)
```

### Step 6: Assign ctheta = value

```python
ctheta = rng.rand(20 * 30) * 2.0 - 1.0
```

### Step 7: Assign beta = value

```python
beta = rng.rand(20 * 30) * 0.8
```

### Step 8: Assign unknown = _get_legen_table(...)

```python
lut, n_fact = _get_legen_table('meg', n_coeff=10, force_calc=True)
```

### Step 9: Assign fun = interp1d(...)

```python
fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, 'nearest', axis=0)
```

### Step 10: Assign coeffs = _comp_sums_meg(...)

```python
coeffs = _comp_sums_meg(beta, ctheta, fun, n_fact, False)
```

### Step 11: Assign unknown = _get_legen_table(...)

```python
lut, n_fact = _get_legen_table('meg', n_coeff=20, force_calc=True)
```

### Step 12: Assign fun = interp1d(...)

```python
fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, 'linear', axis=0)
```

### Step 13: Assign coeffs = _comp_sums_meg(...)

```python
coeffs = _comp_sums_meg(beta, ctheta, fun, n_fact, False)
```

### Step 14: Assign unknown = _get_legen_table(...)

```python
lut, n_fact = _get_legen_table('eeg', n_coeff=nc, force_calc=True)
```

### Step 15: Assign lut_fun = interp1d(...)

```python
lut_fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, interp, axis=0)
```

### Step 16: Assign vals_i = lut_fun(...)

```python
vals_i = lut_fun(xs)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(vals_np[:, 1:vals_i.shape[1] + 1], vals_i, rtol=0.01, atol=0.005)
```

### Step 18: Assign ctheta = value

```python
ctheta = rng.rand(20, 30) * 2.0 - 1.0
```

### Step 19: Assign beta = value

```python
beta = rng.rand(20, 30) * 0.8
```

### Step 20: Assign c1 = _comp_sum_eeg(...)

```python
c1 = _comp_sum_eeg(beta.flatten(), ctheta.flatten(), lut_fun, n_fact)
```

### Step 21: Assign c1 = _reshape_view(...)

```python
c1 = _reshape_view(c1, beta.shape)
```

### Step 22: Assign n = value

```python
n = np.arange(1, n_terms, dtype=float)[:, np.newaxis, np.newaxis]
```

### Step 23: Assign coeffs = np.zeros(...)

```python
coeffs = np.zeros((n_terms,) + beta.shape)
```

### Step 24: Assign unknown = value

```python
coeffs[1:] = np.cumprod([beta] * (n_terms - 1), axis=0) * (2.0 * n + 1.0) * (2.0 * n + 1.0) / n
```

### Step 25: Assign c2 = np.empty(...)

```python
c2 = np.empty((20, 30))
```

### Step 26: Call assert_allclose()

```python
assert_allclose(c1, c2, 0.01, 0.001)
```

### Step 27: Assign unknown = legendre.legval(...)

```python
c2[ci1, ci2] = legendre.legval(ctheta[ci1, ci2], coeffs[:, ci1, ci2])
```


## Complete Example

```python
# Workflow
'Test Legendre polynomial (derivative) equivalence.'
rng = np.random.RandomState(0)
xs = np.linspace(-1.0, 1.0, 1000)
n_terms = 100
vals_np = legendre.legvander(xs, n_terms - 1)
for nc, interp in zip([100, 50], ['nearest', 'linear']):
    lut, n_fact = _get_legen_table('eeg', n_coeff=nc, force_calc=True)
    lut_fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, interp, axis=0)
    vals_i = lut_fun(xs)
    assert_allclose(vals_np[:, 1:vals_i.shape[1] + 1], vals_i, rtol=0.01, atol=0.005)
    ctheta = rng.rand(20, 30) * 2.0 - 1.0
    beta = rng.rand(20, 30) * 0.8
    c1 = _comp_sum_eeg(beta.flatten(), ctheta.flatten(), lut_fun, n_fact)
    c1 = _reshape_view(c1, beta.shape)
    n = np.arange(1, n_terms, dtype=float)[:, np.newaxis, np.newaxis]
    coeffs = np.zeros((n_terms,) + beta.shape)
    coeffs[1:] = np.cumprod([beta] * (n_terms - 1), axis=0) * (2.0 * n + 1.0) * (2.0 * n + 1.0) / n
    c2 = np.empty((20, 30))
    for ci1 in range(20):
        for ci2 in range(30):
            c2[ci1, ci2] = legendre.legval(ctheta[ci1, ci2], coeffs[:, ci1, ci2])
    assert_allclose(c1, c2, 0.01, 0.001)
ctheta = rng.rand(20 * 30) * 2.0 - 1.0
beta = rng.rand(20 * 30) * 0.8
lut, n_fact = _get_legen_table('meg', n_coeff=10, force_calc=True)
fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, 'nearest', axis=0)
coeffs = _comp_sums_meg(beta, ctheta, fun, n_fact, False)
lut, n_fact = _get_legen_table('meg', n_coeff=20, force_calc=True)
fun = interp1d(np.linspace(-1, 1, lut.shape[0]), lut, 'linear', axis=0)
coeffs = _comp_sums_meg(beta, ctheta, fun, n_fact, False)
```

## Next Steps


---

*Source: test_field_interpolation.py:65 | Complexity: Advanced | Last updated: 2026-05-18*