# How To: Temporal Filter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test methods of TemporalFilter.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.decomposition`
- `sklearn.kernel_ridge`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.defaults`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test methods of TemporalFilter.'

```python
'Test methods of TemporalFilter.'
```

**Verification:**
```python
assert_array_equal(filt.fit_transform(X), Xt)
```

### Step 2: Assign X = np.random.rand(...)

```python
X = np.random.rand(5, 5, 1200)
```

**Verification:**
```python
assert X.shape == Xt.shape
```

### Step 3: Assign values = value

```python
values = (('10hz', None, 100.0, 'auto'), (5.0, '10hz', 100.0, 'auto'), (10.0, 20.0, 5.0, 'auto'), (None, None, 100.0, '5hz'))
```

**Verification:**
```python
assert_equal(filt.fit_transform(X).shape, X.shape)
```

### Step 4: Assign X = np.random.rand(...)

```python
X = np.random.rand(101, 500)
```

### Step 5: Assign filt = TemporalFilter(...)

```python
filt = TemporalFilter(l_freq=25.0, h_freq=50.0, sfreq=1000.0, filter_length=150, fir_design='firwin2')
```

### Step 6: Assign filt = TemporalFilter(...)

```python
filt = TemporalFilter(low, high, sf, ltrans, fir_design='firwin')
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, filt.fit_transform, X)
```

### Step 8: Assign filt = TemporalFilter(...)

```python
filt = TemporalFilter(low, high, sfreq=100.0, fir_design='firwin')
```

### Step 9: Assign Xt = filt.fit_transform(...)

```python
Xt = filt.fit_transform(X)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(filt.fit_transform(X), Xt)
```

**Verification:**
```python
assert X.shape == Xt.shape
```

### Step 11: Call filt.transform()

```python
filt.transform('foo')
```

### Step 12: Call assert_equal()

```python
assert_equal(filt.fit_transform(X).shape, X.shape)
```


## Complete Example

```python
# Workflow
'Test methods of TemporalFilter.'
X = np.random.rand(5, 5, 1200)
values = (('10hz', None, 100.0, 'auto'), (5.0, '10hz', 100.0, 'auto'), (10.0, 20.0, 5.0, 'auto'), (None, None, 100.0, '5hz'))
for low, high, sf, ltrans in values:
    filt = TemporalFilter(low, high, sf, ltrans, fir_design='firwin')
    pytest.raises(ValueError, filt.fit_transform, X)
for low, high in ((5.0, 15.0), (None, 15.0), (5.0, None)):
    filt = TemporalFilter(low, high, sfreq=100.0, fir_design='firwin')
    Xt = filt.fit_transform(X)
    assert_array_equal(filt.fit_transform(X), Xt)
    assert X.shape == Xt.shape
with pytest.raises(ValueError):
    filt.transform('foo')
X = np.random.rand(101, 500)
filt = TemporalFilter(l_freq=25.0, h_freq=50.0, sfreq=1000.0, filter_length=150, fir_design='firwin2')
with use_log_level('error'):
    assert_equal(filt.fit_transform(X).shape, X.shape)
```

## Next Steps


---

*Source: test_transformer.py:283 | Complexity: Advanced | Last updated: 2026-05-18*