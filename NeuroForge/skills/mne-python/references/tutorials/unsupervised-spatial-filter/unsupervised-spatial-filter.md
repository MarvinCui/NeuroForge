# How To: Unsupervised Spatial Filter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test unsupervised spatial filter.

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

### Step 1: 'Test unsupervised spatial filter.'

```python
'Test unsupervised spatial filter.'
```

**Verification:**
```python
assert_equal(usf.transform(X).ndim, 3)
```

### Step 2: Assign raw = io.read_raw_fif(...)

```python
raw = io.read_raw_fif(raw_fname)
```

**Verification:**
```python
assert_array_almost_equal(usf.transform(X), usf1.fit_transform(X))
```

### Step 3: Assign events = read_events(...)

```python
events = read_events(event_name)
```

**Verification:**
```python
assert_equal(usf.transform(X).shape[1], n_components)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
```

**Verification:**
```python
assert_array_almost_equal(usf.inverse_transform(usf.transform(X)), X)
```

### Step 5: Assign picks = value

```python
picks = picks[1:13:3]
```

### Step 6: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=None, verbose=False)
```

### Step 7: Assign X = epochs.get_data(...)

```python
X = epochs.get_data(copy=False)
```

### Step 8: Assign usf = UnsupervisedSpatialFilter(...)

```python
usf = UnsupervisedSpatialFilter(KernelRidge(2))
```

### Step 9: Assign n_components = 4

```python
n_components = 4
```

### Step 10: Assign usf = UnsupervisedSpatialFilter(...)

```python
usf = UnsupervisedSpatialFilter(PCA(n_components))
```

### Step 11: Call usf.fit()

```python
usf.fit(X)
```

### Step 12: Assign usf1 = UnsupervisedSpatialFilter(...)

```python
usf1 = UnsupervisedSpatialFilter(PCA(n_components))
```

### Step 13: Call assert_equal()

```python
assert_equal(usf.transform(X).ndim, 3)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(usf.transform(X), usf1.fit_transform(X))
```

### Step 15: Call assert_equal()

```python
assert_equal(usf.transform(X).shape[1], n_components)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(usf.inverse_transform(usf.transform(X)), X)
```

### Step 17: Assign usf = UnsupervisedSpatialFilter(...)

```python
usf = UnsupervisedSpatialFilter(PCA(4), average=True)
```

### Step 18: Call usf.fit_transform()

```python
usf.fit_transform(X)
```

### Step 19: Assign usf = UnsupervisedSpatialFilter(...)

```python
usf = UnsupervisedSpatialFilter(PCA(4), 2)
```

### Step 20: Call usf.fit()

```python
usf.fit(X)
```

### Step 21: Call usf.fit()

```python
usf.fit(X)
```


## Complete Example

```python
# Workflow
'Test unsupervised spatial filter.'
raw = io.read_raw_fif(raw_fname)
events = read_events(event_name)
picks = pick_types(raw.info, meg=True, stim=False, ecg=False, eog=False, exclude='bads')
picks = picks[1:13:3]
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, preload=True, baseline=None, verbose=False)
X = epochs.get_data(copy=False)
usf = UnsupervisedSpatialFilter(KernelRidge(2))
with pytest.raises(ValueError, match='transform'):
    usf.fit(X)
n_components = 4
usf = UnsupervisedSpatialFilter(PCA(n_components))
usf.fit(X)
usf1 = UnsupervisedSpatialFilter(PCA(n_components))
assert_equal(usf.transform(X).ndim, 3)
assert_array_almost_equal(usf.transform(X), usf1.fit_transform(X))
assert_equal(usf.transform(X).shape[1], n_components)
assert_array_almost_equal(usf.inverse_transform(usf.transform(X)), X)
usf = UnsupervisedSpatialFilter(PCA(4), average=True)
usf.fit_transform(X)
usf = UnsupervisedSpatialFilter(PCA(4), 2)
with pytest.raises(TypeError, match='average must be'):
    usf.fit(X)
```

## Next Steps


---

*Source: test_transformer.py:236 | Complexity: Advanced | Last updated: 2026-05-18*