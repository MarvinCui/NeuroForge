# How To: Sphere Construct

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sphere construct

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign s0 = Sphere(...)

```python
s0 = Sphere(xyz=verts)
```

### Step 2: Assign s1 = Sphere(...)

```python
s1 = Sphere(theta=theta, phi=phi)
```

### Step 3: Assign unknown = value

```python
x, y, z = verts.T
```

### Step 4: Assign s2 = Sphere(...)

```python
s2 = Sphere(x=x, y=y, z=z)
```

### Step 5: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, s1.theta)
```

### Step 6: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, s2.theta)
```

### Step 7: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, theta)
```

### Step 8: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, s1.phi)
```

### Step 9: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, s2.phi)
```

### Step 10: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, phi)
```


## Complete Example

```python
# Workflow
s0 = Sphere(xyz=verts)
s1 = Sphere(theta=theta, phi=phi)
x, y, z = verts.T
s2 = Sphere(x=x, y=y, z=z)
nt.assert_array_almost_equal(s0.theta, s1.theta)
nt.assert_array_almost_equal(s0.theta, s2.theta)
nt.assert_array_almost_equal(s0.theta, theta)
nt.assert_array_almost_equal(s0.phi, s1.phi)
nt.assert_array_almost_equal(s0.phi, s2.phi)
nt.assert_array_almost_equal(s0.phi, phi)
```

## Next Steps


---

*Source: test_sphere.py:58 | Complexity: Advanced | Last updated: 2026-05-18*