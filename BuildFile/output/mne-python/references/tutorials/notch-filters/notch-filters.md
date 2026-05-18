# How To: Notch Filters

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test notch filters.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: method, filter_length, line_freq, tol
```

## Step-by-Step Guide

### Step 1: 'Test notch filters.'

```python
'Test notch filters.'
```

**Verification:**
```python
assert len(out) == 4, 'Detected frequencies not logged properly'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_array_almost_equal(out, line_freqs)
```

### Step 3: Assign sfreq = 487

```python
sfreq = 487
```

**Verification:**
```python
assert_almost_equal(new_power, orig_power, tol)
```

### Step 4: Assign sig_len_secs = 21

```python
sig_len_secs = 21
```

### Step 5: Assign t = value

```python
t = np.arange(0, int(round(sig_len_secs * sfreq))) / sfreq
```

### Step 6: Assign a = rng.randn(...)

```python
a = rng.randn(int(sig_len_secs * sfreq))
```

### Step 7: Assign orig_power = np.sqrt(...)

```python
orig_power = np.sqrt(np.mean(a ** 2))
```

### Step 8: Assign new_power = np.sqrt(...)

```python
new_power = np.sqrt(sum_squared(b) / b.size)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(new_power, orig_power, tol)
```

### Step 10: Assign b = notch_filter(...)

```python
b = notch_filter(a, sfreq, line_freq, filter_length, method=method, verbose=True)
```

### Step 11: Assign out = value

```python
out = [line.strip().split(':')[0] for line in log_file.getvalue().split('\n') if line.startswith(' ')]
```

**Verification:**
```python
assert len(out) == 4, 'Detected frequencies not logged properly'
```

### Step 12: Assign out = np.array(...)

```python
out = np.array(out, float)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(out, line_freqs)
```

### Step 14: Call notch_filter()

```python
notch_filter(a, sfreq, None, kind)
```


## Complete Example

```python
# Setup
# Fixtures: method, filter_length, line_freq, tol

# Workflow
'Test notch filters.'
rng = np.random.RandomState(0)
sfreq = 487
sig_len_secs = 21
t = np.arange(0, int(round(sig_len_secs * sfreq))) / sfreq
a = rng.randn(int(sig_len_secs * sfreq))
orig_power = np.sqrt(np.mean(a ** 2))
a += np.sum([np.sin(2 * np.pi * f * t) for f in line_freqs], axis=0)
for kind in ('fir', 'iir'):
    with pytest.raises(ValueError, match='freqs=None can only be used wi'):
        notch_filter(a, sfreq, None, kind)
with catch_logging() as log_file:
    b = notch_filter(a, sfreq, line_freq, filter_length, method=method, verbose=True)
if line_freq is None:
    out = [line.strip().split(':')[0] for line in log_file.getvalue().split('\n') if line.startswith(' ')]
    assert len(out) == 4, 'Detected frequencies not logged properly'
    out = np.array(out, float)
    assert_array_almost_equal(out, line_freqs)
new_power = np.sqrt(sum_squared(b) / b.size)
assert_almost_equal(new_power, orig_power, tol)
```

## Next Steps


---

*Source: test_filter.py:338 | Complexity: Advanced | Last updated: 2026-05-18*