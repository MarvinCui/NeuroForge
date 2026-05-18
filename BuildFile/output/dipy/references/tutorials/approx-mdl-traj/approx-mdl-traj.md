# How To: Approx Mdl Traj

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test approx mdl traj

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.streamline`
- `time`


## Step-by-Step Guide

### Step 1: Assign t = np.linspace(...)

```python
t = np.linspace(0, 1.75 * 2 * np.pi, 100)
```

**Verification:**
```python
assert_equal(len(xyza1), 10)
```

### Step 2: Assign x = np.sin(...)

```python
x = np.sin(t)
```

**Verification:**
```python
assert_equal(len(xyza2), 8)
```

### Step 3: Assign y = np.cos(...)

```python
y = np.cos(t)
```

**Verification:**
```python
assert_array_almost_equal(xyza1, np.array([[0.0, 1.0, 0.0], [0.939692621, 0.342020143, 1.22173048], [0.64278761, -0.766044443, 2.44346095], [-0.5, -0.866025404, 3.66519143], [-0.984807753, 0.173648178, 4.88692191], [-0.173648178, 0.984807753, 6.10865238], [0.866025404, 0.5, 7.33038286], [0.766044443, -0.64278761, 8.55211333], [-0.342020143, -0.939692621, 9.77384381], [-1.0, -4.2862638e-16, 10.9955743]]))
```

### Step 4: Assign z = t

```python
z = t
```

**Verification:**
```python
assert_array_almost_equal(xyza2, np.array([[0.0, 1.0, 0.0], [0.995471923, -0.0950560433, 1.6659961], [-0.189251244, -0.981928697, 3.33199221], [-0.959492974, 0.281732557, 4.99798831], [0.371662456, 0.928367933, 6.66398442], [0.888835449, -0.458226522, 8.32998052], [-0.540640817, -0.841253533, 9.99597663], [-1.0, -4.2862638e-16, 10.9955743]]))
```

### Step 5: Assign xyz = value

```python
xyz = np.vstack((x, y, z)).T
```

### Step 6: Assign xyza1 = pf.approximate_mdl_trajectory(...)

```python
xyza1 = pf.approximate_mdl_trajectory(xyz, alpha=1.0)
```

### Step 7: Assign xyza2 = pf.approximate_mdl_trajectory(...)

```python
xyza2 = pf.approximate_mdl_trajectory(xyz, alpha=2.0)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(xyza1), 10)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(xyza2), 8)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(xyza1, np.array([[0.0, 1.0, 0.0], [0.939692621, 0.342020143, 1.22173048], [0.64278761, -0.766044443, 2.44346095], [-0.5, -0.866025404, 3.66519143], [-0.984807753, 0.173648178, 4.88692191], [-0.173648178, 0.984807753, 6.10865238], [0.866025404, 0.5, 7.33038286], [0.766044443, -0.64278761, 8.55211333], [-0.342020143, -0.939692621, 9.77384381], [-1.0, -4.2862638e-16, 10.9955743]]))
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(xyza2, np.array([[0.0, 1.0, 0.0], [0.995471923, -0.0950560433, 1.6659961], [-0.189251244, -0.981928697, 3.33199221], [-0.959492974, 0.281732557, 4.99798831], [0.371662456, 0.928367933, 6.66398442], [0.888835449, -0.458226522, 8.32998052], [-0.540640817, -0.841253533, 9.99597663], [-1.0, -4.2862638e-16, 10.9955743]]))
```


## Complete Example

```python
# Workflow
t = np.linspace(0, 1.75 * 2 * np.pi, 100)
x = np.sin(t)
y = np.cos(t)
z = t
xyz = np.vstack((x, y, z)).T
xyza1 = pf.approximate_mdl_trajectory(xyz, alpha=1.0)
xyza2 = pf.approximate_mdl_trajectory(xyz, alpha=2.0)
assert_equal(len(xyza1), 10)
assert_equal(len(xyza2), 8)
assert_array_almost_equal(xyza1, np.array([[0.0, 1.0, 0.0], [0.939692621, 0.342020143, 1.22173048], [0.64278761, -0.766044443, 2.44346095], [-0.5, -0.866025404, 3.66519143], [-0.984807753, 0.173648178, 4.88692191], [-0.173648178, 0.984807753, 6.10865238], [0.866025404, 0.5, 7.33038286], [0.766044443, -0.64278761, 8.55211333], [-0.342020143, -0.939692621, 9.77384381], [-1.0, -4.2862638e-16, 10.9955743]]))
assert_array_almost_equal(xyza2, np.array([[0.0, 1.0, 0.0], [0.995471923, -0.0950560433, 1.6659961], [-0.189251244, -0.981928697, 3.33199221], [-0.959492974, 0.281732557, 4.99798831], [0.371662456, 0.928367933, 6.66398442], [0.888835449, -0.458226522, 8.32998052], [-0.540640817, -0.841253533, 9.99597663], [-1.0, -4.2862638e-16, 10.9955743]]))
```

## Next Steps


---

*Source: test_distances.py:230 | Complexity: Advanced | Last updated: 2026-05-18*