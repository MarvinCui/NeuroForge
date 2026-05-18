# How To: Invalid Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test invalid transform

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.transforms`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign transform = Transform(...)

```python
transform = Transform()
```

**Verification:**
```python
assert_raises(ValueError, transform.jacobian, theta, x)
```

### Step 2: Assign theta = np.ndarray(...)

```python
theta = np.ndarray(3)
```

**Verification:**
```python
assert_raises(ValueError, transform.get_identity_parameters)
```

### Step 3: Assign x = np.ndarray(...)

```python
x = np.ndarray(3)
```

**Verification:**
```python
assert_raises(ValueError, transform.param_to_matrix, theta)
```

### Step 4: Call assert_raises()

```python
assert_raises(ValueError, transform.jacobian, theta, x)
```

**Verification:**
```python
assert_equal(actual, expected)
```

### Step 5: Call assert_raises()

```python
assert_raises(ValueError, transform.get_identity_parameters)
```

**Verification:**
```python
assert_equal(actual, expected)
```

### Step 6: Call assert_raises()

```python
assert_raises(ValueError, transform.param_to_matrix, theta)
```

### Step 7: Assign expected = value

```python
expected = -1
```

### Step 8: Assign actual = transform.get_number_of_parameters(...)

```python
actual = transform.get_number_of_parameters()
```

### Step 9: Call assert_equal()

```python
assert_equal(actual, expected)
```

### Step 10: Assign actual = transform.get_dim(...)

```python
actual = transform.get_dim()
```

### Step 11: Call assert_equal()

```python
assert_equal(actual, expected)
```


## Complete Example

```python
# Workflow
transform = Transform()
theta = np.ndarray(3)
x = np.ndarray(3)
assert_raises(ValueError, transform.jacobian, theta, x)
assert_raises(ValueError, transform.get_identity_parameters)
assert_raises(ValueError, transform.param_to_matrix, theta)
expected = -1
actual = transform.get_number_of_parameters()
assert_equal(actual, expected)
actual = transform.get_dim()
assert_equal(actual, expected)
```

## Next Steps


---

*Source: test_transforms.py:257 | Complexity: Advanced | Last updated: 2026-05-18*