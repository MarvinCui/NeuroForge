# How To: Hemisphere Constructor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hemisphere constructor

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

### Step 1: Assign s0 = HemiSphere(...)

```python
s0 = HemiSphere(xyz=verts)
```

### Step 2: Assign s1 = HemiSphere(...)

```python
s1 = HemiSphere(theta=theta, phi=phi)
```

### Step 3: Assign unknown = value

```python
x, y, z = verts.T
```

### Step 4: Assign s2 = HemiSphere(...)

```python
s2 = HemiSphere(x=x, y=y, z=z)
```

### Step 5: Assign uniq_verts = value

```python
uniq_verts = verts[::2].T
```

### Step 6: Assign unknown = cart2sphere(...)

```python
rU, thetaU, phiU = cart2sphere(*uniq_verts)
```

### Step 7: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, s1.theta)
```

### Step 8: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, s2.theta)
```

### Step 9: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.theta, thetaU)
```

### Step 10: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, s1.phi)
```

### Step 11: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, s2.phi)
```

### Step 12: Call nt.assert_array_almost_equal()

```python
nt.assert_array_almost_equal(s0.phi, phiU)
```


## Complete Example

```python
# Workflow
s0 = HemiSphere(xyz=verts)
s1 = HemiSphere(theta=theta, phi=phi)
x, y, z = verts.T
s2 = HemiSphere(x=x, y=y, z=z)
uniq_verts = verts[::2].T
rU, thetaU, phiU = cart2sphere(*uniq_verts)
nt.assert_array_almost_equal(s0.theta, s1.theta)
nt.assert_array_almost_equal(s0.theta, s2.theta)
nt.assert_array_almost_equal(s0.theta, thetaU)
nt.assert_array_almost_equal(s0.phi, s1.phi)
nt.assert_array_almost_equal(s0.phi, s2.phi)
nt.assert_array_almost_equal(s0.phi, phiU)
```

## Next Steps


---

*Source: test_sphere.py:198 | Complexity: Advanced | Last updated: 2026-05-18*