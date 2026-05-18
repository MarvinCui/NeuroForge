# How To: Perpendicular Directions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test perpendicular directions

## Prerequisites

**Required Modules:**
- `itertools`
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`
- `dipy.testing.spherepoints`


## Step-by-Step Guide

### Step 1: Assign num = 35

```python
num = 35
```

**Verification:**
```python
assert_equal(num, len(pd))
```

### Step 2: Assign vectors_v = np.zeros(...)

```python
vectors_v = np.zeros((4, 3))
```

**Verification:**
```python
assert_almost_equal(cos_angle, 0)
```

### Step 3: Assign unknown = value

```python
vectors_v[3] = [1, 0, 0]
```

**Verification:**
```python
assert_almost_equal(rest, 0)
```

### Step 4: Assign theta = random.uniform(...)

```python
theta = random.uniform(0, np.pi)
```

### Step 5: Assign phi = random.uniform(...)

```python
phi = random.uniform(0, 2 * np.pi)
```

### Step 6: Assign unknown = sphere2cart(...)

```python
vectors_v[v] = sphere2cart(1.0, theta, phi)
```

### Step 7: Assign pd = perpendicular_directions(...)

```python
pd = perpendicular_directions(vector_v, num=num, half=False)
```

### Step 8: Call assert_equal()

```python
assert_equal(num, len(pd))
```

### Step 9: Assign delta_a = value

```python
delta_a = 2.0 * np.pi / num
```

### Step 10: Assign cos_angle = np.dot(...)

```python
cos_angle = np.dot(d, vector_v)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(cos_angle, 0)
```

### Step 12: Assign angle = np.arccos(...)

```python
angle = np.arccos(np.dot(pd[0], d))
```

### Step 13: Assign rest = value

```python
rest = angle % delta_a
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(rest, 0)
```

### Step 15: Assign rest = value

```python
rest = rest - delta_a
```


## Complete Example

```python
# Workflow
num = 35
vectors_v = np.zeros((4, 3))
for v in range(4):
    theta = random.uniform(0, np.pi)
    phi = random.uniform(0, 2 * np.pi)
    vectors_v[v] = sphere2cart(1.0, theta, phi)
vectors_v[3] = [1, 0, 0]
for vector_v in vectors_v:
    pd = perpendicular_directions(vector_v, num=num, half=False)
    assert_equal(num, len(pd))
    for d in pd:
        cos_angle = np.dot(d, vector_v)
        assert_almost_equal(cos_angle, 0)
    delta_a = 2.0 * np.pi / num
    for d in pd[1:]:
        angle = np.arccos(np.dot(pd[0], d))
        rest = angle % delta_a
        if rest > delta_a * 0.99:
            rest = rest - delta_a
        assert_almost_equal(rest, 0)
```

## Next Steps


---

*Source: test_geometry.py:286 | Complexity: Advanced | Last updated: 2026-05-18*