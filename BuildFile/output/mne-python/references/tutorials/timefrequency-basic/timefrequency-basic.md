# How To: Timefrequency Basic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test TimeFrequency.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.base`
- `sklearn.utils.estimator_checks`
- `mne.decoding.time_frequency`


## Step-by-Step Guide

### Step 1: 'Test TimeFrequency.'

```python
'Test TimeFrequency.'
```

**Verification:**
```python
assert not hasattr(tf, 'fitted_')
```

### Step 2: Assign n_freqs = 3

```python
n_freqs = 3
```

**Verification:**
```python
assert tf.fitted_
```

### Step 3: Assign freqs = value

```python
freqs = [20, 21, 22]
```

**Verification:**
```python
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times])
```

### Step 4: Assign tf = TimeFrequency(...)

```python
tf = TimeFrequency(freqs, sfreq=100)
```

**Verification:**
```python
assert_array_equal(Xt.shape, [n_epochs, n_freqs, n_times])
```

### Step 5: Assign unknown = value

```python
n_epochs, n_chans, n_times = (10, 2, 100)
```

**Verification:**
```python
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times // 2])
```

### Step 6: Assign X = np.random.rand(...)

```python
X = np.random.rand(n_epochs, n_chans, n_times)
```

### Step 7: Assign tf = clone(...)

```python
tf = clone(tf)
```

### Step 8: Assign freqs_array = np.array(...)

```python
freqs_array = np.array(np.asarray(freqs))
```

### Step 9: Assign tf = TimeFrequency(...)

```python
tf = TimeFrequency(freqs_array, 100, 'morlet', freqs_array / 5.0)
```

### Step 10: Call clone()

```python
clone(tf)
```

**Verification:**
```python
assert not hasattr(tf, 'fitted_')
```

### Step 11: Call tf.fit()

```python
tf.fit(X, None)
```

**Verification:**
```python
assert tf.fitted_
```

### Step 12: Assign tf = TimeFrequency(...)

```python
tf = TimeFrequency(freqs, sfreq=100)
```

### Step 13: Call tf.fit_transform()

```python
tf.fit_transform(X, None)
```

### Step 14: Assign Xt = tf.transform(...)

```python
Xt = tf.transform(X)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times])
```

### Step 16: Assign Xt = tf.fit_transform(...)

```python
Xt = tf.fit_transform(X[:, 0, :])
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(Xt.shape, [n_epochs, n_freqs, n_times])
```

### Step 18: Assign tf = TimeFrequency(...)

```python
tf = TimeFrequency(freqs, sfreq=100, decim=2)
```

### Step 19: Assign Xt = tf.fit_transform(...)

```python
Xt = tf.fit_transform(X)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times // 2])
```

### Step 21: Assign tf = TimeFrequency(...)

```python
tf = TimeFrequency(freqs, output=output)
```

### Step 22: Call tf.fit()

```python
tf.fit(X)
```


## Complete Example

```python
# Workflow
'Test TimeFrequency.'
n_freqs = 3
freqs = [20, 21, 22]
tf = TimeFrequency(freqs, sfreq=100)
n_epochs, n_chans, n_times = (10, 2, 100)
X = np.random.rand(n_epochs, n_chans, n_times)
for output in ['avg_power', 'foo', None]:
    tf = TimeFrequency(freqs, output=output)
    with pytest.raises(ValueError, match='Invalid value'):
        tf.fit(X)
tf = clone(tf)
freqs_array = np.array(np.asarray(freqs))
tf = TimeFrequency(freqs_array, 100, 'morlet', freqs_array / 5.0)
clone(tf)
assert not hasattr(tf, 'fitted_')
tf.fit(X, None)
assert tf.fitted_
tf = TimeFrequency(freqs, sfreq=100)
tf.fit_transform(X, None)
Xt = tf.transform(X)
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times])
Xt = tf.fit_transform(X[:, 0, :])
assert_array_equal(Xt.shape, [n_epochs, n_freqs, n_times])
tf = TimeFrequency(freqs, sfreq=100, decim=2)
Xt = tf.fit_transform(X)
assert_array_equal(Xt.shape, [n_epochs, n_chans, n_freqs, n_times // 2])
```

## Next Steps


---

*Source: test_time_frequency.py:18 | Complexity: Advanced | Last updated: 2026-05-18*