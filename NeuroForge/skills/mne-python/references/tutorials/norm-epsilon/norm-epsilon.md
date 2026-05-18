# How To: Norm Epsilon

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computation of espilon norm on TF coefficients.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.inverse_sparse.mxne_optim`
- `mne.time_frequency._stft`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test computation of espilon norm on TF coefficients.'

```python
'Test computation of espilon norm on TF coefficients.'
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), 0.0)
```

### Step 2: Assign tstep = np.array(...)

```python
tstep = np.array([2])
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
```

### Step 3: Assign wsize = np.array(...)

```python
wsize = np.array([4])
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
```

### Step 4: Assign n_times = 10

```python
n_times = 10
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi) ** 2, stft_norm2(Y.reshape(-1, n_freqs[0], n_steps[0])))
```

### Step 5: Assign n_steps = np.ceil.astype(...)

```python
n_steps = np.ceil(n_times / tstep.astype(float)).astype(int)
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), norm_epsilon(Y, l1_ratio, phi, w_time=w_time))
```

### Step 6: Assign n_freqs = value

```python
n_freqs = wsize // 2 + 1
```

**Verification:**
```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi, w_space=1, w_time=np.ones(n_coefs.item())) / mult, norm_epsilon(Y, l1_ratio, phi, w_space=mult, w_time=mult * np.ones(n_coefs.item())))
```

### Step 7: Assign n_coefs = value

```python
n_coefs = n_steps * n_freqs
```

### Step 8: Assign phi = _Phi(...)

```python
phi = _Phi(wsize, tstep, n_coefs, n_times)
```

### Step 9: Assign Y = np.zeros(...)

```python
Y = np.zeros((n_steps * n_freqs).item())
```

### Step 10: Assign l1_ratio = 0.03

```python
l1_ratio = 0.03
```

### Step 11: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), 0.0)
```

### Step 12: Assign unknown = 2.0

```python
Y[0] = 2.0
```

### Step 13: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
```

### Step 14: Assign l1_ratio = 1.0

```python
l1_ratio = 1.0
```

### Step 15: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
```

### Step 16: Assign Y = np.arange(...)

```python
Y = np.arange((n_steps * n_freqs).item())
```

### Step 17: Assign l1_ratio = 0.0

```python
l1_ratio = 0.0
```

### Step 18: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi) ** 2, stft_norm2(Y.reshape(-1, n_freqs[0], n_steps[0])))
```

### Step 19: Assign l1_ratio = 0.03

```python
l1_ratio = 0.03
```

### Step 20: Assign w_time = np.ones(...)

```python
w_time = np.ones(n_coefs[0])
```

### Step 21: Assign Y = np.abs(...)

```python
Y = np.abs(np.random.randn(n_coefs[0]))
```

### Step 22: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi), norm_epsilon(Y, l1_ratio, phi, w_time=w_time))
```

### Step 23: Assign Y = value

```python
Y = np.arange(n_coefs.item()) + 1
```

### Step 24: Assign mult = 2.0

```python
mult = 2.0
```

### Step 25: Call assert_allclose()

```python
assert_allclose(norm_epsilon(Y, l1_ratio, phi, w_space=1, w_time=np.ones(n_coefs.item())) / mult, norm_epsilon(Y, l1_ratio, phi, w_space=mult, w_time=mult * np.ones(n_coefs.item())))
```


## Complete Example

```python
# Workflow
'Test computation of espilon norm on TF coefficients.'
tstep = np.array([2])
wsize = np.array([4])
n_times = 10
n_steps = np.ceil(n_times / tstep.astype(float)).astype(int)
n_freqs = wsize // 2 + 1
n_coefs = n_steps * n_freqs
phi = _Phi(wsize, tstep, n_coefs, n_times)
Y = np.zeros((n_steps * n_freqs).item())
l1_ratio = 0.03
assert_allclose(norm_epsilon(Y, l1_ratio, phi), 0.0)
Y[0] = 2.0
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
l1_ratio = 1.0
assert_allclose(norm_epsilon(Y, l1_ratio, phi), np.max(Y))
Y = np.arange((n_steps * n_freqs).item())
l1_ratio = 0.0
assert_allclose(norm_epsilon(Y, l1_ratio, phi) ** 2, stft_norm2(Y.reshape(-1, n_freqs[0], n_steps[0])))
l1_ratio = 0.03
w_time = np.ones(n_coefs[0])
Y = np.abs(np.random.randn(n_coefs[0]))
assert_allclose(norm_epsilon(Y, l1_ratio, phi), norm_epsilon(Y, l1_ratio, phi, w_time=w_time))
Y = np.arange(n_coefs.item()) + 1
mult = 2.0
assert_allclose(norm_epsilon(Y, l1_ratio, phi, w_space=1, w_time=np.ones(n_coefs.item())) / mult, norm_epsilon(Y, l1_ratio, phi, w_space=mult, w_time=mult * np.ones(n_coefs.item())))
```

## Next Steps


---

*Source: test_mxne_optim.py:168 | Complexity: Advanced | Last updated: 2026-05-18*