# How To: Verbose Arg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test controlling output with the ``verbose`` argument.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.base`
- `sklearn.discriminant_analysis`
- `sklearn.ensemble`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.multiclass`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne.decoding.search_light`
- `mne.decoding.transformer`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: capsys, n_jobs, verbose
```

## Step-by-Step Guide

### Step 1: 'Test controlling output with the ``verbose`` argument.'

```python
'Test controlling output with the ``verbose`` argument.'
```

**Verification:**
```python
assert all((channel == '' for channel in (stdout, stderr)))
```

### Step 2: Assign unknown = make_data(...)

```python
X, y = make_data()
```

**Verification:**
```python
assert any((len(channel) > 0 for channel in (stdout, stderr)))
```

### Step 3: Assign clf = SVC(...)

```python
clf = SVC()
```

### Step 4: Assign estimator = estimator_object(...)

```python
estimator = estimator_object(clf, n_jobs=n_jobs, verbose=verbose)
```

### Step 5: Assign estimator = estimator.fit(...)

```python
estimator = estimator.fit(X, y)
```

### Step 6: Call estimator.score()

```python
estimator.score(X, y)
```

### Step 7: Call estimator.predict()

```python
estimator.predict(X)
```

### Step 8: Assign unknown = capsys.readouterr(...)

```python
stdout, stderr = capsys.readouterr()
```

**Verification:**
```python
assert all((channel == '' for channel in (stdout, stderr)))
```


## Complete Example

```python
# Setup
# Fixtures: capsys, n_jobs, verbose

# Workflow
'Test controlling output with the ``verbose`` argument.'
X, y = make_data()
clf = SVC()
with use_log_level(True):
    for estimator_object in [SlidingEstimator, GeneralizingEstimator]:
        estimator = estimator_object(clf, n_jobs=n_jobs, verbose=verbose)
        estimator = estimator.fit(X, y)
        estimator.score(X, y)
        estimator.predict(X)
        stdout, stderr = capsys.readouterr()
        if isinstance(verbose, bool) and (not verbose):
            assert all((channel == '' for channel in (stdout, stderr)))
        else:
            assert any((len(channel) > 0 for channel in (stdout, stderr)))
```

## Next Steps


---

*Source: test_search_light.py:299 | Complexity: Advanced | Last updated: 2026-05-18*