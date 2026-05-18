# How To: Non Square Infomax

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test non-square infomax.

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

### Step 1: 'Test non-square infomax.'

```python
'Test non-square infomax.'
```

**Verification:**
```python
assert_almost_equal(m, s_.T.dot(mixing_))
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
```

### Step 3: Assign n_samples = 200

```python
n_samples = 200
```

**Verification:**
```python
assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```

### Step 4: Assign t = np.linspace(...)

```python
t = np.linspace(0, 100, n_samples)
```

### Step 5: Assign s1 = np.sin(...)

```python
s1 = np.sin(t)
```

### Step 6: Assign s2 = np.ceil(...)

```python
s2 = np.ceil(np.sin(np.pi * t))
```

### Step 7: Assign s = value

```python
s = np.c_[s1, s2].T
```

### Step 8: Call center_and_norm()

```python
center_and_norm(s)
```

### Step 9: Assign unknown = s

```python
s1, s2 = s
```

### Step 10: Assign n_observed = 6

```python
n_observed = 6
```

### Step 11: Assign mixing = rng.randn(...)

```python
mixing = rng.randn(n_observed, 2)
```

### Step 12: Assign m = np.dot(...)

```python
m = np.dot(mixing, s)
```

### Step 13: Call center_and_norm()

```python
center_and_norm(m)
```

### Step 14: Assign m = value

```python
m = m.T
```

### Step 15: Assign m = _get_pca.fit_transform(...)

```python
m = _get_pca(rng).fit_transform(m)
```

### Step 16: Assign unmixing_ = infomax(...)

```python
unmixing_ = infomax(m, random_state=rng, extended=True)
```

### Step 17: Assign s_ = np.dot(...)

```python
s_ = np.dot(unmixing_, m.T)
```

### Step 18: Assign mixing_ = pinv(...)

```python
mixing_ = pinv(unmixing_.T)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(m, s_.T.dot(mixing_))
```

### Step 20: Call center_and_norm()

```python
center_and_norm(s_)
```

### Step 21: Assign unknown = s_

```python
s1_, s2_ = s_
```

### Step 22: Assign unknown = s_

```python
s2_, s1_ = s_
```

### Step 23: Call assert_almost_equal()

```python
assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
```

### Step 24: Call assert_almost_equal()

```python
assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```


## Complete Example

```python
# Workflow
'Test non-square infomax.'
rng = np.random.RandomState(0)
n_samples = 200
t = np.linspace(0, 100, n_samples)
s1 = np.sin(t)
s2 = np.ceil(np.sin(np.pi * t))
s = np.c_[s1, s2].T
center_and_norm(s)
s1, s2 = s
n_observed = 6
mixing = rng.randn(n_observed, 2)
for add_noise in (False, True):
    m = np.dot(mixing, s)
    if add_noise:
        m += 0.1 * rng.randn(n_observed, n_samples)
    center_and_norm(m)
    m = m.T
    m = _get_pca(rng).fit_transform(m)
    unmixing_ = infomax(m, random_state=rng, extended=True)
    s_ = np.dot(unmixing_, m.T)
    mixing_ = pinv(unmixing_.T)
    assert_almost_equal(m, s_.T.dot(mixing_))
    center_and_norm(s_)
    s1_, s2_ = s_
    if abs(np.dot(s1_, s2)) > abs(np.dot(s1_, s1)):
        s2_, s1_ = s_
    s1_ *= np.sign(np.dot(s1_, s1))
    s2_ *= np.sign(np.dot(s2_, s2))
    if not add_noise:
        assert_almost_equal(np.dot(s1_, s1) / n_samples, 1, decimal=2)
        assert_almost_equal(np.dot(s2_, s2) / n_samples, 1, decimal=2)
```

## Next Steps


---

*Source: test_infomax.py:133 | Complexity: Advanced | Last updated: 2026-05-18*