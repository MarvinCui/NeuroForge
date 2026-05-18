# How To: Get Coef Multiclass Full

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test a full example with pattern extraction.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn`
- `sklearn.base`
- `sklearn.base`
- `sklearn.base`
- `sklearn.decomposition`
- `sklearn.discriminant_analysis`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.multiclass`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.base`
- `mne.decoding.search_light`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: n_classes, n_channels, n_times
```

## Step-by-Step Guide

### Step 1: 'Test a full example with pattern extraction.'

```python
'Test a full example with pattern extraction.'
```

**Verification:**
```python
assert scores.shape == want
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((10 * n_classes, n_channels, n_times))
```

**Verification:**
```python
assert_array_less(limit, scores)
```

### Step 3: Assign events = np.zeros(...)

```python
events = np.zeros((len(data), 3), int)
```

**Verification:**
```python
assert patterns.shape == (n_classes, n_channels, n_times)
```

### Step 4: Assign unknown = np.arange(...)

```python
events[:, 0] = np.arange(len(events))
```

**Verification:**
```python
assert_allclose(patterns[:, 1:], 0.0, atol=1e-07)
```

### Step 5: Assign unknown = value

```python
events[:, 2] = data[:, 0, 0]
```

### Step 6: Assign info = create_info(...)

```python
info = create_info(n_channels, 1000.0, 'eeg')
```

### Step 7: Assign epochs = EpochsArray(...)

```python
epochs = EpochsArray(data, info, events, tmin=0)
```

### Step 8: Assign clf = make_pipeline(...)

```python
clf = make_pipeline(Scaler(epochs.info), Vectorizer(), LinearModel(OneVsRestClassifier(LogisticRegression(random_state=0))))
```

### Step 9: Assign scorer = 'roc_auc_ovr_weighted'

```python
scorer = 'roc_auc_ovr_weighted'
```

### Step 10: Assign time_gen = GeneralizingEstimator(...)

```python
time_gen = GeneralizingEstimator(clf, scorer, verbose=True)
```

### Step 11: Assign X = epochs.get_data(...)

```python
X = epochs.get_data(copy=False)
```

### Step 12: Assign y = value

```python
y = epochs.events[:, 2]
```

### Step 13: Assign n_splits = 3

```python
n_splits = 3
```

### Step 14: Assign cv = StratifiedKFold(...)

```python
cv = StratifiedKFold(n_splits=n_splits)
```

### Step 15: Assign scores = cross_val_multiscore(...)

```python
scores = cross_val_multiscore(time_gen, X, y, cv=cv, verbose=True)
```

### Step 16: Assign want = value

```python
want = (n_splits,)
```

**Verification:**
```python
assert scores.shape == want
```

### Step 17: Assign limit = value

```python
limit = 0.7 if platform.system() == 'Windows' else 0.8
```

### Step 18: Call assert_array_less()

```python
assert_array_less(limit, scores)
```

### Step 19: Call clf.fit()

```python
clf.fit(X, y)
```

### Step 20: Assign patterns = get_coef(...)

```python
patterns = get_coef(clf, 'patterns_', inverse_transform=True)
```

**Verification:**
```python
assert patterns.shape == (n_classes, n_channels, n_times)
```

### Step 21: Call assert_allclose()

```python
assert_allclose(patterns[:, 1:], 0.0, atol=1e-07)
```

### Step 22: Assign unknown = ii

```python
data[ii * 10:(ii + 1) * 10, 0] = ii
```


## Complete Example

```python
# Setup
# Fixtures: n_classes, n_channels, n_times

# Workflow
'Test a full example with pattern extraction.'
data = np.zeros((10 * n_classes, n_channels, n_times))
for ii in range(n_classes):
    data[ii * 10:(ii + 1) * 10, 0] = ii
events = np.zeros((len(data), 3), int)
events[:, 0] = np.arange(len(events))
events[:, 2] = data[:, 0, 0]
info = create_info(n_channels, 1000.0, 'eeg')
epochs = EpochsArray(data, info, events, tmin=0)
clf = make_pipeline(Scaler(epochs.info), Vectorizer(), LinearModel(OneVsRestClassifier(LogisticRegression(random_state=0))))
scorer = 'roc_auc_ovr_weighted'
time_gen = GeneralizingEstimator(clf, scorer, verbose=True)
X = epochs.get_data(copy=False)
y = epochs.events[:, 2]
n_splits = 3
cv = StratifiedKFold(n_splits=n_splits)
scores = cross_val_multiscore(time_gen, X, y, cv=cv, verbose=True)
want = (n_splits,)
if n_times > 1:
    want += (n_times, n_times)
assert scores.shape == want
limit = 0.7 if platform.system() == 'Windows' else 0.8
assert_array_less(limit, scores)
clf.fit(X, y)
patterns = get_coef(clf, 'patterns_', inverse_transform=True)
assert patterns.shape == (n_classes, n_channels, n_times)
assert_allclose(patterns[:, 1:], 0.0, atol=1e-07)
```

## Next Steps


---

*Source: test_base.py:437 | Complexity: Advanced | Last updated: 2026-05-18*