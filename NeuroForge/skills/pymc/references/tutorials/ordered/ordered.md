# How To: Ordered

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ordered

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.pytensorf`
- `pymc.testing`
- `numpy`


## Step-by-Step Guide

### Step 1: Call check_vector_transform()

```python
check_vector_transform(tr.ordered, SortedVector(6))
```

**Verification:**
```python
assert_array_equal(np.diff(vals) >= 0, True)
```

### Step 2: Call check_jacobian_det()

```python
check_jacobian_det(tr.ordered, Vector(R, 2), pt.vector, floatX(np.array([0, 0])), elemwise=False)
```

**Verification:**
```python
assert_array_equal(vals > 0, True)
```

### Step 3: Assign vals = get_values(...)

```python
vals = get_values(tr.ordered, Vector(R, 3), pt.vector, floatX(np.zeros(3)))
```

**Verification:**
```python
assert_array_equal(np.diff(vals) >= 0, True)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(np.diff(vals) >= 0, True)
```

**Verification:**
```python
assert_array_equal(vals > 0, True)
```

### Step 5: Assign vals = get_values(...)

```python
vals = get_values(tr.Ordered(positive=True), Vector(R, 3), pt.vector, floatX(np.zeros(3)))
```

**Verification:**
```python
assert_array_equal(np.diff(vals) <= 0, True)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(vals > 0, True)
```

**Verification:**
```python
assert_allclose(vals, ord.backward(ord.forward(vals)).eval())
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(np.diff(vals) >= 0, True)
```

### Step 8: Assign vals = get_values(...)

```python
vals = get_values(tr.Ordered(positive=True, ascending=False), Vector(R, 3), pt.vector, floatX(np.zeros(3)))
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(vals > 0, True)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(np.diff(vals) <= 0, True)
```

### Step 11: Assign unknown = value

```python
ord, vals = (tr.Ordered(positive=True, ascending=False), np.array([0.3, 0.2, 0.1]))
```

### Step 12: Call assert_allclose()

```python
assert_allclose(vals, ord.backward(ord.forward(vals)).eval())
```

### Step 13: Call check_jacobian_det()

```python
check_jacobian_det(tr.Ordered(positive=True, ascending=False), Vector(R, 2), pt.vector, floatX(np.array([1, 1])), elemwise=False)
```


## Complete Example

```python
# Workflow
check_vector_transform(tr.ordered, SortedVector(6))
check_jacobian_det(tr.ordered, Vector(R, 2), pt.vector, floatX(np.array([0, 0])), elemwise=False)
vals = get_values(tr.ordered, Vector(R, 3), pt.vector, floatX(np.zeros(3)))
assert_array_equal(np.diff(vals) >= 0, True)
vals = get_values(tr.Ordered(positive=True), Vector(R, 3), pt.vector, floatX(np.zeros(3)))
assert_array_equal(vals > 0, True)
assert_array_equal(np.diff(vals) >= 0, True)
vals = get_values(tr.Ordered(positive=True, ascending=False), Vector(R, 3), pt.vector, floatX(np.zeros(3)))
assert_array_equal(vals > 0, True)
assert_array_equal(np.diff(vals) <= 0, True)
ord, vals = (tr.Ordered(positive=True, ascending=False), np.array([0.3, 0.2, 0.1]))
assert_allclose(vals, ord.backward(ord.forward(vals)).eval())
check_jacobian_det(tr.Ordered(positive=True, ascending=False), Vector(R, 2), pt.vector, floatX(np.array([1, 1])), elemwise=False)
```

## Next Steps


---

*Source: test_transform.py:255 | Complexity: Advanced | Last updated: 2026-05-18*