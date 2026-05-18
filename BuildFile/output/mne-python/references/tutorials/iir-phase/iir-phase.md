# How To: Iir Phase

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test IIR filter phase.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy.signal`
- `scipy.signal`
- `mne`
- `mne._fiff.pick`
- `mne.filter`
- `mne.io`
- `mne.utils`
- `mne.cuda`


## Step-by-Step Guide

### Step 1: 'Test IIR filter phase.'

```python
'Test IIR filter phase.'
```

**Verification:**
```python
assert_allclose(sig_f[:ind_one], np.zeros(ind_one))
```

### Step 2: Assign unknown = value

```python
sig, sfreq, ind_one = (np.zeros(101), 10, 50)
```

**Verification:**
```python
assert np.linalg.norm(sig) > np.linalg.norm(sig_f)
```

### Step 3: Assign unknown = 1

```python
sig[ind_one] = 1
```

**Verification:**
```python
assert_allclose(sig_fb, sig_fb[::-1], rtol=1e-05, atol=1e-06)
```

### Step 4: Assign iir_params = dict(...)

```python
iir_params = dict(ftype='butter', order=2, output='sos')
```

**Verification:**
```python
assert np.argmax(sig_fb) == ind_one
```

### Step 5: Assign sig_f = filter_data(...)

```python
sig_f = filter_data(sig, sfreq, 0.6, None, method='iir', phase='forward', iir_params=iir_params)
```

**Verification:**
```python
assert np.linalg.norm(sig_f) > np.linalg.norm(sig_fb)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(sig_f[:ind_one], np.zeros(ind_one))
```

**Verification:**
```python
assert np.linalg.norm(sig) > np.linalg.norm(sig_f)
```

### Step 7: Assign sig_fb = filter_data(...)

```python
sig_fb = filter_data(sig, sfreq, 0.6, None, method='iir', phase='zero', iir_params=iir_params)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(sig_fb, sig_fb[::-1], rtol=1e-05, atol=1e-06)
```

**Verification:**
```python
assert np.argmax(sig_fb) == ind_one
```


## Complete Example

```python
# Workflow
'Test IIR filter phase.'
sig, sfreq, ind_one = (np.zeros(101), 10, 50)
sig[ind_one] = 1
iir_params = dict(ftype='butter', order=2, output='sos')
sig_f = filter_data(sig, sfreq, 0.6, None, method='iir', phase='forward', iir_params=iir_params)
assert_allclose(sig_f[:ind_one], np.zeros(ind_one))
assert np.linalg.norm(sig) > np.linalg.norm(sig_f)
sig_fb = filter_data(sig, sfreq, 0.6, None, method='iir', phase='zero', iir_params=iir_params)
assert_allclose(sig_fb, sig_fb[::-1], rtol=1e-05, atol=1e-06)
assert np.argmax(sig_fb) == ind_one
assert np.linalg.norm(sig_f) > np.linalg.norm(sig_fb)
```

## Next Steps


---

*Source: test_filter.py:297 | Complexity: Advanced | Last updated: 2026-05-18*