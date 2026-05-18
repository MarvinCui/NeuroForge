# How To: Angle Axis2Quat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test angle axis2quat

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign q = nq.angle_axis2quat(...)

```python
q = nq.angle_axis2quat(0, [1, 0, 0])
```

**Verification:**
```python
assert_array_equal(q, [1, 0, 0, 0])
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(q, [1, 0, 0, 0])
```

**Verification:**
```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```

### Step 3: Assign q = nq.angle_axis2quat(...)

```python
q = nq.angle_axis2quat(np.pi, [1, 0, 0])
```

**Verification:**
```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```

**Verification:**
```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```

### Step 5: Assign q = nq.angle_axis2quat(...)

```python
q = nq.angle_axis2quat(np.pi, [1, 0, 0], True)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```

### Step 7: Assign q = nq.angle_axis2quat(...)

```python
q = nq.angle_axis2quat(np.pi, [2, 0, 0], False)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(q, [0, 1, 0, 0])
```


## Complete Example

```python
# Workflow
q = nq.angle_axis2quat(0, [1, 0, 0])
assert_array_equal(q, [1, 0, 0, 0])
q = nq.angle_axis2quat(np.pi, [1, 0, 0])
assert_array_almost_equal(q, [0, 1, 0, 0])
q = nq.angle_axis2quat(np.pi, [1, 0, 0], True)
assert_array_almost_equal(q, [0, 1, 0, 0])
q = nq.angle_axis2quat(np.pi, [2, 0, 0], False)
assert_array_almost_equal(q, [0, 1, 0, 0])
```

## Next Steps


---

*Source: test_quaternions.py:207 | Complexity: Advanced | Last updated: 2026-05-18*