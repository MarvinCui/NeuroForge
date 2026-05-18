# How To: Grad Matrix

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test for matricial form of gradient.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `test_same_api`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test for matricial form of gradient.'

```python
'Test for matricial form of gradient.'
```

**Verification:**
```python
assert_almost_equal(gradient(image_buffer)[grad_mask], np.dot(G, v))
```

### Step 2: Assign unknown = _make_data(...)

```python
_, _, w, mask, *_ = _make_data()
```

### Step 3: Assign G = get_gradient_matrix(...)

```python
G = get_gradient_matrix(w.size, mask)
```

### Step 4: Assign image_buffer = np.zeros(...)

```python
image_buffer = np.zeros(mask.shape)
```

### Step 5: Assign grad_mask = np.array(...)

```python
grad_mask = np.array([mask for _ in range(mask.ndim)])
```

### Step 6: Assign v = value

```python
v = rng.random(w.size) * rng.integers(1000)
```

### Step 7: Assign unknown = v

```python
image_buffer[mask] = v
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(gradient(image_buffer)[grad_mask], np.dot(G, v))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test for matricial form of gradient.'
_, _, w, mask, *_ = _make_data()
G = get_gradient_matrix(w.size, mask)
image_buffer = np.zeros(mask.shape)
grad_mask = np.array([mask for _ in range(mask.ndim)])
for _ in range(10):
    v = rng.random(w.size) * rng.integers(1000)
    image_buffer[mask] = v
    assert_almost_equal(gradient(image_buffer)[grad_mask], np.dot(G, v))
```

## Next Steps


---

*Source: test_graph_net.py:62 | Complexity: Advanced | Last updated: 2026-05-18*