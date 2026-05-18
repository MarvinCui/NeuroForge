# How To: Jacobian Functions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test jacobian functions

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.transforms`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign h = 1e-08

```python
h = 1e-08
```

**Verification:**
```python
assert_array_almost_equal(actual, expected, decimal=5)
```

### Step 2: Assign nsamples = 50

```python
nsamples = 50
```

**Verification:**
```python
assert_raises(ValueError, transform.jacobian, theta, x)
```

### Step 3: Assign n = transform.get_number_of_parameters(...)

```python
n = transform.get_number_of_parameters()
```

### Step 4: Assign dim = transform.get_dim(...)

```python
dim = transform.get_dim()
```

### Step 5: Assign expected = np.empty(...)

```python
expected = np.empty((dim, n))
```

### Step 6: Assign theta = rng.uniform(...)

```python
theta = rng.uniform(size=(n,))
```

### Step 7: Assign T = transform.param_to_matrix(...)

```python
T = transform.param_to_matrix(theta)
```

### Step 8: Assign n = transform.get_number_of_parameters(...)

```python
n = transform.get_number_of_parameters()
```

### Step 9: Assign theta = np.zeros(...)

```python
theta = np.zeros(n + 1)
```

### Step 10: Assign x = np.zeros(...)

```python
x = np.zeros(dim)
```

### Step 11: Call assert_raises()

```python
assert_raises(ValueError, transform.jacobian, theta, x)
```

### Step 12: Assign x = value

```python
x = 255 * (rng.uniform(size=(dim,)) - 0.5)
```

### Step 13: Assign actual = transform.jacobian(...)

```python
actual = transform.jacobian(theta, x)
```

### Step 14: Assign x_hom = np.ones(...)

```python
x_hom = np.ones(dim + 1)
```

### Step 15: Assign unknown = value

```python
x_hom[:dim] = x[:]
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(actual, expected, decimal=5)
```

### Step 17: Assign dtheta = theta.copy(...)

```python
dtheta = theta.copy()
```

### Step 18: Assign dT = np.array(...)

```python
dT = np.array(transform.param_to_matrix(dtheta))
```

### Step 19: Assign g = value

```python
g = (dT - T).dot(x_hom) / h
```

### Step 20: Assign unknown = value

```python
expected[:, i] = g[:dim]
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
h = 1e-08
nsamples = 50
for transform in regtransforms.values():
    n = transform.get_number_of_parameters()
    dim = transform.get_dim()
    expected = np.empty((dim, n))
    theta = rng.uniform(size=(n,))
    T = transform.param_to_matrix(theta)
    for _ in range(nsamples):
        x = 255 * (rng.uniform(size=(dim,)) - 0.5)
        actual = transform.jacobian(theta, x)
        x_hom = np.ones(dim + 1)
        x_hom[:dim] = x[:]
        for i in range(n):
            dtheta = theta.copy()
            dtheta[i] += h
            dT = np.array(transform.param_to_matrix(dtheta))
            g = (dT - T).dot(x_hom) / h
            expected[:, i] = g[:dim]
        assert_array_almost_equal(actual, expected, decimal=5)
for transform in regtransforms.values():
    n = transform.get_number_of_parameters()
    theta = np.zeros(n + 1)
    x = np.zeros(dim)
    assert_raises(ValueError, transform.jacobian, theta, x)
```

## Next Steps


---

*Source: test_transforms.py:218 | Complexity: Advanced | Last updated: 2026-05-18*