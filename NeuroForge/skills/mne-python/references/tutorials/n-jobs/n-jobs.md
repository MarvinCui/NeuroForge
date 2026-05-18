# How To: N Jobs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test resampling against SciPy.

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
# Fixtures: n_jobs, capsys
```

## Step-by-Step Guide

### Step 1: 'Test resampling against SciPy.'

```python
'Test resampling against SciPy.'
```

**Verification:**
```python
assert_allclose(y1, y2)
```

### Step 2: Assign joblib = pytest.importorskip(...)

```python
joblib = pytest.importorskip('joblib')
```

**Verification:**
```python
assert 'Parallel(' not in out
```

### Step 3: Assign x = np.random.RandomState.randn(...)

```python
x = np.random.RandomState(0).randn(4, 100)
```

**Verification:**
```python
assert 'Parallel(' not in err
```

### Step 4: Assign y1 = resample(...)

```python
y1 = resample(x, 2, 1, n_jobs=None)
```

**Verification:**
```python
assert_allclose(y1, y2)
```

### Step 5: Assign y2 = resample(...)

```python
y2 = resample(x, 2, 1, n_jobs=n_jobs)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(y1, y2)
```

### Step 7: Call capsys.readouterr()

```python
capsys.readouterr()
```

### Step 8: Assign unknown = capsys.readouterr(...)

```python
out, err = capsys.readouterr()
```

**Verification:**
```python
assert 'Parallel(' not in out
```

### Step 9: Assign y2 = filter_data(...)

```python
y2 = filter_data(x, 100.0, 0, 40, n_jobs=n_jobs, verbose=True)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(y1, y2)
```

### Step 11: Assign y1 = filter_data(...)

```python
y1 = filter_data(x, 100.0, 0, 40, n_jobs=None, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: n_jobs, capsys

# Workflow
'Test resampling against SciPy.'
joblib = pytest.importorskip('joblib')
x = np.random.RandomState(0).randn(4, 100)
y1 = resample(x, 2, 1, n_jobs=None)
y2 = resample(x, 2, 1, n_jobs=n_jobs)
assert_allclose(y1, y2)
capsys.readouterr()
with joblib.parallel_config(backend='loky', n_jobs=1):
    y1 = filter_data(x, 100.0, 0, 40, n_jobs=None, verbose=True)
out, err = capsys.readouterr()
assert 'Parallel(' not in out
assert 'Parallel(' not in err
y2 = filter_data(x, 100.0, 0, 40, n_jobs=n_jobs, verbose=True)
assert_allclose(y1, y2)
```

## Next Steps


---

*Source: test_filter.py:419 | Complexity: Advanced | Last updated: 2026-05-18*