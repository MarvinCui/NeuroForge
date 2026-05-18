# How To: Morlet

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test morlet with and without zero mean.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`

**Setup Required:**
```python
# Fixtures: sfreq, freq, n_cycles
```

## Step-by-Step Guide

### Step 1: 'Test morlet with and without zero mean.'

```python
'Test morlet with and without zero mean.'
```

**Verification:**
```python
assert np.abs(np.mean(np.real(Wz))) < 1e-05
```

### Step 2: Assign Wz = morlet(...)

```python
Wz = morlet(sfreq, freq, n_cycles, zero_mean=True)
```

**Verification:**
```python
assert np.abs(np.mean(np.real(W))) > 0.001
```

### Step 3: Assign W = morlet(...)

```python
W = morlet(sfreq, freq, n_cycles, zero_mean=False)
```

**Verification:**
```python
assert np.abs(np.mean(np.real(W))) < 1e-05
```

### Step 4: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(W), np.sqrt(2), atol=1e-06)
```

**Verification:**
```python
assert_allclose(np.linalg.norm(W), np.sqrt(2), atol=1e-06)
```

### Step 5: Assign M = len(...)

```python
M = len(W)
```

**Verification:**
```python
assert_allclose(W, Ws)
```

### Step 6: Assign w = n_cycles

```python
w = n_cycles
```

**Verification:**
```python
assert_allclose(fwhm_formula, fwhm_empirical, atol=3 / sfreq)
```

### Step 7: Assign s = value

```python
s = w * sfreq / (2 * freq * np.pi)
```

### Step 8: Assign Ws = value

```python
Ws = _morlet2(M, s, w) * np.sqrt(2)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(W, Ws)
```

### Step 10: Assign fwhm_formula = fwhm(...)

```python
fwhm_formula = fwhm(freq, n_cycles)
```

### Step 11: Assign half_max = value

```python
half_max = np.abs(W).max() / 2.0
```

### Step 12: Assign fwhm_empirical = value

```python
fwhm_empirical = (np.abs(W) >= half_max).sum() / sfreq
```

### Step 13: Call assert_allclose()

```python
assert_allclose(fwhm_formula, fwhm_empirical, atol=3 / sfreq)
```

**Verification:**
```python
assert np.abs(np.mean(np.real(W))) > 0.001
```


## Complete Example

```python
# Setup
# Fixtures: sfreq, freq, n_cycles

# Workflow
'Test morlet with and without zero mean.'
Wz = morlet(sfreq, freq, n_cycles, zero_mean=True)
W = morlet(sfreq, freq, n_cycles, zero_mean=False)
assert np.abs(np.mean(np.real(Wz))) < 1e-05
if n_cycles == 2:
    assert np.abs(np.mean(np.real(W))) > 0.001
else:
    assert np.abs(np.mean(np.real(W))) < 1e-05
assert_allclose(np.linalg.norm(W), np.sqrt(2), atol=1e-06)
M = len(W)
w = n_cycles
s = w * sfreq / (2 * freq * np.pi)
Ws = _morlet2(M, s, w) * np.sqrt(2)
assert_allclose(W, Ws)
fwhm_formula = fwhm(freq, n_cycles)
half_max = np.abs(W).max() / 2.0
fwhm_empirical = (np.abs(W) >= half_max).sum() / sfreq
assert_allclose(fwhm_formula, fwhm_empirical, atol=3 / sfreq)
```

## Next Steps


---

*Source: test_tfr.py:114 | Complexity: Advanced | Last updated: 2026-05-18*