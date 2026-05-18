# How To: Mahalanobis2

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mahalanobis2

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.linalg`
- `scipy.stats`
- `numpy.testing`
- `scipy.stats`
- `nilearn._utils.data_gen`
- `nilearn.glm._utils`
- `nilearn.glm.first_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 50

```python
n = 50
```

**Verification:**
```python
assert np.allclose(mah, f_mah)
```

### Step 2: Assign x = rng.standard_normal(...)

```python
x = rng.standard_normal(size=(n, 3))
```

### Step 3: Assign Aa = np.zeros(...)

```python
Aa = np.zeros([n, n, 3])
```

### Step 4: Assign i = rng.integers(...)

```python
i = rng.integers(3)
```

### Step 5: Assign mah = np.dot(...)

```python
mah = np.dot(x[:, i], np.dot(spl.inv(Aa[:, :, i]), x[:, i]))
```

### Step 6: Assign f_mah = value

```python
f_mah = multiple_mahalanobis(x, Aa)[i]
```

**Verification:**
```python
assert np.allclose(mah, f_mah)
```

### Step 7: Assign A = rng.standard_normal(...)

```python
A = rng.standard_normal(size=(120, n))
```

### Step 8: Assign A = np.dot(...)

```python
A = np.dot(A.T, A)
```

### Step 9: Assign unknown = A

```python
Aa[:, :, i] = A
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 50
x = rng.standard_normal(size=(n, 3))
Aa = np.zeros([n, n, 3])
for i in range(3):
    A = rng.standard_normal(size=(120, n))
    A = np.dot(A.T, A)
    Aa[:, :, i] = A
i = rng.integers(3)
mah = np.dot(x[:, i], np.dot(spl.inv(Aa[:, :, i]), x[:, i]))
f_mah = multiple_mahalanobis(x, Aa)[i]
assert np.allclose(mah, f_mah)
```

## Next Steps


---

*Source: test_utils.py:174 | Complexity: Advanced | Last updated: 2026-05-18*