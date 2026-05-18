# How To: Rank Deficiency

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test signals that are rank deficient.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy`
- `numpy.fft`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.utils.estimator_checks`
- `mne.decoding`
- `mne.decoding.receptive_field`
- `mne.decoding.time_delaying_ridge`
- `mne.fixes`


## Step-by-Step Guide

### Step 1: 'Test signals that are rank deficient.'

```python
'Test signals that are rank deficient.'
```

**Verification:**
```python
assert_equal(y.shape, pred.shape)
```

### Step 2: Assign N = 256

```python
N = 256
```

**Verification:**
```python
assert corr > 0.995
```

### Step 3: Assign fs = 1.0

```python
fs = 1.0
```

### Step 4: Assign unknown = value

```python
tmin, tmax = (-50, 100)
```

### Step 5: Assign reg = 0.1

```python
reg = 0.1
```

### Step 6: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 7: Assign eeg = rng.randn(...)

```python
eeg = rng.randn(N, 1)
```

### Step 8: Assign eeg = rfft(...)

```python
eeg = rfft(eeg, axis=0)
```

### Step 9: Assign unknown = 0

```python
eeg[N // 4:] = 0
```

### Step 10: Assign eeg = irfft(...)

```python
eeg = irfft(eeg, axis=0)
```

### Step 11: Assign win = np.hanning(...)

```python
win = np.hanning(N // 8)
```

### Step 12: Assign y = np.apply_along_axis(...)

```python
y = np.apply_along_axis(np.convolve, 0, eeg, win, mode='same')
```

### Step 13: Assign rf = ReceptiveField(...)

```python
rf = ReceptiveField(tmin, tmax, fs, estimator=est, patterns=True)
```

### Step 14: Call rf.fit()

```python
rf.fit(eeg, y)
```

### Step 15: Assign pred = rf.predict(...)

```python
pred = rf.predict(eeg)
```

### Step 16: Call assert_equal()

```python
assert_equal(y.shape, pred.shape)
```

### Step 17: Assign corr = value

```python
corr = np.corrcoef(y.ravel(), pred.ravel())[0, 1]
```

**Verification:**
```python
assert corr > 0.995
```


## Complete Example

```python
# Workflow
'Test signals that are rank deficient.'
N = 256
fs = 1.0
tmin, tmax = (-50, 100)
reg = 0.1
rng = np.random.RandomState(0)
eeg = rng.randn(N, 1)
eeg *= 100
eeg = rfft(eeg, axis=0)
eeg[N // 4:] = 0
eeg = irfft(eeg, axis=0)
win = np.hanning(N // 8)
win /= win.mean()
y = np.apply_along_axis(np.convolve, 0, eeg, win, mode='same')
y += rng.randn(*y.shape) * 100
for est in (Ridge(reg), reg):
    rf = ReceptiveField(tmin, tmax, fs, estimator=est, patterns=True)
    rf.fit(eeg, y)
    pred = rf.predict(eeg)
    assert_equal(y.shape, pred.shape)
    corr = np.corrcoef(y.ravel(), pred.ravel())[0, 1]
    assert corr > 0.995
```

## Next Steps


---

*Source: test_receptive_field.py:85 | Complexity: Advanced | Last updated: 2026-05-18*