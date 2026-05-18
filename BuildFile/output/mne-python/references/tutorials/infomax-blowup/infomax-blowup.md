# How To: Infomax Blowup

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the infomax algorithm blowup condition.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne.preprocessing.infomax_`
- `mne.utils`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: 'Test the infomax algorithm blowup condition.'

```python
'Test the infomax algorithm blowup condition.'
```

**Verification:**
```python
assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(0)
```

**Verification:**
```python
assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```

### Step 3: Assign n_samples = 100

```python
n_samples = 100
```

### Step 4: Assign s1 = value

```python
s1 = (2 * np.sin(np.linspace(0, 100, n_samples)) > 0) - 1
```

### Step 5: Assign s2 = stats.t.rvs(...)

```python
s2 = stats.t.rvs(1, size=n_samples)
```

### Step 6: Assign s = value

```python
s = np.c_[s1, s2].T
```

### Step 7: Call center_and_norm()

```python
center_and_norm(s)
```

### Step 8: Assign unknown = s

```python
s1, s2 = s
```

### Step 9: Assign phi = 0.6

```python
phi = 0.6
```

### Step 10: Assign mixing = np.array(...)

```python
mixing = np.array([[np.cos(phi), np.sin(phi)], [np.sin(phi), -np.cos(phi)]])
```

### Step 11: Assign m = np.dot(...)

```python
m = np.dot(mixing, s)
```

### Step 12: Call center_and_norm()

```python
center_and_norm(m)
```

### Step 13: Assign X = _get_pca.fit_transform(...)

```python
X = _get_pca().fit_transform(m.T)
```

### Step 14: Assign k_ = infomax(...)

```python
k_ = infomax(X, extended=True, l_rate=0.1)
```

### Step 15: Assign s_ = np.dot(...)

```python
s_ = np.dot(k_, X.T)
```

### Step 16: Call center_and_norm()

```python
center_and_norm(s_)
```

### Step 17: Assign unknown = s_

```python
s1_, s2_ = s_
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```

### Step 20: Assign unknown = s_

```python
s2_, s1_ = s_
```


## Complete Example

```python
# Workflow
'Test the infomax algorithm blowup condition.'
np.random.seed(0)
n_samples = 100
s1 = (2 * np.sin(np.linspace(0, 100, n_samples)) > 0) - 1
s2 = stats.t.rvs(1, size=n_samples)
s = np.c_[s1, s2].T
center_and_norm(s)
s1, s2 = s
phi = 0.6
mixing = np.array([[np.cos(phi), np.sin(phi)], [np.sin(phi), -np.cos(phi)]])
m = np.dot(mixing, s)
center_and_norm(m)
X = _get_pca().fit_transform(m.T)
k_ = infomax(X, extended=True, l_rate=0.1)
s_ = np.dot(k_, X.T)
center_and_norm(s_)
s1_, s2_ = s_
if abs(np.dot(s1_, s2)) > abs(np.dot(s1_, s1)):
    s2_, s1_ = s_
s1_ *= np.sign(np.dot(s1_, s1))
s2_ *= np.sign(np.dot(s2_, s2))
assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```

## Next Steps


---

*Source: test_infomax.py:34 | Complexity: Advanced | Last updated: 2026-05-18*