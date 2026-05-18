# How To: Xdawn Decoding Performance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test decoding performance and extracted pattern on synthetic data.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.io`
- `mne.decoding.xdawn`
- `mne.preprocessing.xdawn`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `mne.decoding`


## Step-by-Step Guide

### Step 1: 'Test decoding performance and extracted pattern on synthetic data.'

```python
'Test decoding performance and extracted pattern on synthetic data.'
```

**Verification:**
```python
assert_allclose(cv_accuracy_xdawn, expected_accuracy, atol=0.01)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert np.abs(r) > 0.99
```

### Step 3: Assign n_xdawn_comps = 3

```python
n_xdawn_comps = 3
```

### Step 4: Assign expected_accuracy = 0.98

```python
expected_accuracy = 0.98
```

### Step 5: Assign unknown = _simulate_erplike_mixed_data(...)

```python
epochs, mixing_mat = _simulate_erplike_mixed_data(n_epochs=100)
```

### Step 6: Assign y = value

```python
y = epochs.events[:, 2]
```

### Step 7: Assign xdawn_pipe = make_pipeline(...)

```python
xdawn_pipe = make_pipeline(Xdawn(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
```

### Step 8: Assign xdawn_trans_pipe = make_pipeline(...)

```python
xdawn_trans_pipe = make_pipeline(XdawnTransformer(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
```

### Step 9: Assign cv = KFold(...)

```python
cv = KFold(n_splits=3, shuffle=False)
```

### Step 10: Assign predictions = np.empty_like(...)

```python
predictions = np.empty_like(y, dtype=float)
```

### Step 11: Assign cv_accuracy_xdawn = accuracy_score(...)

```python
cv_accuracy_xdawn = accuracy_score(y, predictions)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(cv_accuracy_xdawn, expected_accuracy, atol=0.01)
```

### Step 13: Assign fitted_xdawn = value

```python
fitted_xdawn = pipe.steps[0][1]
```

### Step 14: Call pipe.fit()

```python
pipe.fit(X[train], y[train])
```

### Step 15: Assign unknown = pipe.predict(...)

```python
predictions[test] = pipe.predict(X[test])
```

### Step 16: Assign relev_patterns = np.concatenate(...)

```python
relev_patterns = np.concatenate([comps[[0]] for comps in fitted_xdawn.patterns_.values()])
```

### Step 17: Assign pick_patterns = fitted_xdawn._subset_multi_components(...)

```python
pick_patterns = fitted_xdawn._subset_multi_components(name='patterns')
```

### Step 18: Assign relev_patterns = value

```python
relev_patterns = pick_patterns[::n_xdawn_comps]
```

### Step 19: Assign unknown = stats.pearsonr(...)

```python
r, _ = stats.pearsonr(relev_patterns[i, :], mixing_mat[0, :])
```

**Verification:**
```python
assert np.abs(r) > 0.99
```


## Complete Example

```python
# Workflow
'Test decoding performance and extracted pattern on synthetic data.'
pytest.importorskip('sklearn')
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
from sklearn.model_selection import KFold
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import MinMaxScaler
from mne.decoding import Vectorizer
n_xdawn_comps = 3
expected_accuracy = 0.98
epochs, mixing_mat = _simulate_erplike_mixed_data(n_epochs=100)
y = epochs.events[:, 2]
xdawn_pipe = make_pipeline(Xdawn(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
xdawn_trans_pipe = make_pipeline(XdawnTransformer(n_components=n_xdawn_comps), Vectorizer(), MinMaxScaler(), LogisticRegression(solver='liblinear'))
cv = KFold(n_splits=3, shuffle=False)
for pipe, X in ((xdawn_pipe, epochs), (xdawn_trans_pipe, epochs.get_data(copy=False))):
    predictions = np.empty_like(y, dtype=float)
    for train, test in cv.split(X, y):
        pipe.fit(X[train], y[train])
        predictions[test] = pipe.predict(X[test])
    cv_accuracy_xdawn = accuracy_score(y, predictions)
    assert_allclose(cv_accuracy_xdawn, expected_accuracy, atol=0.01)
    fitted_xdawn = pipe.steps[0][1]
    if isinstance(fitted_xdawn, Xdawn):
        relev_patterns = np.concatenate([comps[[0]] for comps in fitted_xdawn.patterns_.values()])
    else:
        pick_patterns = fitted_xdawn._subset_multi_components(name='patterns')
        relev_patterns = pick_patterns[::n_xdawn_comps]
    for i in range(len(relev_patterns)):
        r, _ = stats.pearsonr(relev_patterns[i, :], mixing_mat[0, :])
        assert np.abs(r) > 0.99
```

## Next Steps


---

*Source: test_xdawn.py:352 | Complexity: Advanced | Last updated: 2026-05-18*