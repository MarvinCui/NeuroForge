# How To: Stft

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test stft and istft tight frame property.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne.time_frequency`
- `mne.time_frequency._stft`

**Setup Required:**
```python
# Fixtures: T, wsize, tstep, f
```

## Step-by-Step Guide

### Step 1: 'Test stft and istft tight frame property.'

```python
'Test stft and istft tight frame property.'
```

**Verification:**
```python
assert X.shape[1] == len(freqs)
```

### Step 2: Assign sfreq = 1000.0

```python
sfreq = 1000.0
```

**Verification:**
```python
assert np.all(freqs >= 0.0)
```

### Step 3: Assign t = np.arange.astype(...)

```python
t = np.arange(T).astype(np.float64)
```

**Verification:**
```python
assert np.abs(max_freq - f) < 1.0
```

### Step 4: Assign x = np.sin(...)

```python
x = np.sin(2 * np.pi * f * t / sfreq)
```

**Verification:**
```python
assert_array_almost_equal(x, xp, decimal=6)
```

### Step 5: Assign x = np.array(...)

```python
x = np.array([x, x + 1.0])
```

**Verification:**
```python
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
```

### Step 6: Assign X = stft(...)

```python
X = stft(x, wsize, tstep)
```

**Verification:**
```python
assert X.shape[1] == len(freqs)
```

### Step 7: Assign xp = istft(...)

```python
xp = istft(X, tstep, Tx=T)
```

**Verification:**
```python
assert np.all(freqs >= 0.0)
```

### Step 8: Assign freqs = stftfreq(...)

```python
freqs = stftfreq(wsize, sfreq=sfreq)
```

**Verification:**
```python
assert_array_almost_equal(x, xp, decimal=6)
```

### Step 9: Assign max_freq = value

```python
max_freq = freqs[np.argmax(np.sum(np.abs(X[0]) ** 2, axis=1))]
```

**Verification:**
```python
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(x, xp, decimal=6)
```

**Verification:**
```python
assert xp.shape == x.shape
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
```

### Step 12: Assign x = np.random.randn(...)

```python
x = np.random.randn(2, T)
```

### Step 13: Assign wsize = 16

```python
wsize = 16
```

### Step 14: Assign tstep = 8

```python
tstep = 8
```

### Step 15: Assign X = stft(...)

```python
X = stft(x, wsize, tstep)
```

### Step 16: Assign xp = istft(...)

```python
xp = istft(X, tstep, Tx=T)
```

### Step 17: Assign freqs = stftfreq(...)

```python
freqs = stftfreq(wsize, sfreq=1000)
```

### Step 18: Assign max_freq = value

```python
max_freq = freqs[np.argmax(np.sum(np.abs(X[0]) ** 2, axis=1))]
```

**Verification:**
```python
assert X.shape[1] == len(freqs)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(x, xp, decimal=6)
```

### Step 20: Call assert_almost_equal()

```python
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
```

### Step 21: Assign x = np.zeros(...)

```python
x = np.zeros((0, T))
```

### Step 22: Assign X = stft(...)

```python
X = stft(x, wsize, tstep)
```

### Step 23: Assign xp = istft(...)

```python
xp = istft(X, tstep, T)
```

**Verification:**
```python
assert xp.shape == x.shape
```


## Complete Example

```python
# Setup
# Fixtures: T, wsize, tstep, f

# Workflow
'Test stft and istft tight frame property.'
sfreq = 1000.0
t = np.arange(T).astype(np.float64)
x = np.sin(2 * np.pi * f * t / sfreq)
x = np.array([x, x + 1.0])
X = stft(x, wsize, tstep)
xp = istft(X, tstep, Tx=T)
freqs = stftfreq(wsize, sfreq=sfreq)
max_freq = freqs[np.argmax(np.sum(np.abs(X[0]) ** 2, axis=1))]
assert X.shape[1] == len(freqs)
assert np.all(freqs >= 0.0)
assert np.abs(max_freq - f) < 1.0
assert_array_almost_equal(x, xp, decimal=6)
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
x = np.random.randn(2, T)
wsize = 16
tstep = 8
X = stft(x, wsize, tstep)
xp = istft(X, tstep, Tx=T)
freqs = stftfreq(wsize, sfreq=1000)
max_freq = freqs[np.argmax(np.sum(np.abs(X[0]) ** 2, axis=1))]
assert X.shape[1] == len(freqs)
assert np.all(freqs >= 0.0)
assert_array_almost_equal(x, xp, decimal=6)
assert_almost_equal(np.sqrt(stft_norm2(X)), [linalg.norm(xx) for xx in x], decimal=6)
x = np.zeros((0, T))
X = stft(x, wsize, tstep)
xp = istft(X, tstep, T)
assert xp.shape == x.shape
```

## Next Steps


---

*Source: test_stft.py:18 | Complexity: Advanced | Last updated: 2026-05-18*