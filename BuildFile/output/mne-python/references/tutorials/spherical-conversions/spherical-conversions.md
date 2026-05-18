# How To: Spherical Conversions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test spherical harmonic conversions.

## Prerequisites

**Required Modules:**
- `pathlib`
- `re`
- `contextlib`
- `functools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.chpi`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.maxwell`
- `mne.rank`
- `mne.utils`
- `scipy.io`


## Step-by-Step Guide

### Step 1: 'Test spherical harmonic conversions.'

```python
'Test spherical harmonic conversions.'
```

**Verification:**
```python
assert_allclose(_sh_negate(sph, order), sph_harm_y(degree, -order, pol, az))
```

### Step 2: Assign unknown = np.meshgrid(...)

```python
az, pol = np.meshgrid(np.linspace(0, 2 * np.pi, 30), np.linspace(0, np.pi, 20))
```

**Verification:**
```python
assert_allclose(sph, sph_2, atol=1e-07)
```

### Step 3: Assign sph = sph_harm_y(...)

```python
sph = sph_harm_y(degree, order, pol, az)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(_sh_negate(sph, order), sph_harm_y(degree, -order, pol, az))
```

### Step 5: Assign sph_real_pos = _sh_complex_to_real(...)

```python
sph_real_pos = _sh_complex_to_real(sph, order)
```

### Step 6: Assign sph_real_neg = _sh_complex_to_real(...)

```python
sph_real_neg = _sh_complex_to_real(sph, -order)
```

### Step 7: Assign sph_2 = _sh_real_to_complex(...)

```python
sph_2 = _sh_real_to_complex([sph_real_pos, sph_real_neg], order)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(sph, sph_2, atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test spherical harmonic conversions.'
az, pol = np.meshgrid(np.linspace(0, 2 * np.pi, 30), np.linspace(0, np.pi, 20))
for degree in range(1, int_order):
    for order in range(0, degree + 1):
        sph = sph_harm_y(degree, order, pol, az)
        assert_allclose(_sh_negate(sph, order), sph_harm_y(degree, -order, pol, az))
        sph_real_pos = _sh_complex_to_real(sph, order)
        sph_real_neg = _sh_complex_to_real(sph, -order)
        sph_2 = _sh_real_to_complex([sph_real_pos, sph_real_neg], order)
        assert_allclose(sph, sph_2, atol=1e-07)
```

## Next Steps


---

*Source: test_maxwell.py:488 | Complexity: Advanced | Last updated: 2026-05-18*