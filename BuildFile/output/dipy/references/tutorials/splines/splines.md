# How To: Splines

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test splines

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign t = np.linspace(...)

```python
t = np.linspace(0, 1.75 * 2 * np.pi, 100)
```

### Step 2: Assign x = np.sin(...)

```python
x = np.sin(t)
```

### Step 3: Assign y = np.cos(...)

```python
y = np.cos(t)
```

### Step 4: Assign z = t

```python
z = t
```

### Step 5: Assign xyz = value

```python
xyz = np.vstack((x, y, z)).T
```

### Step 6: Call tm.spline()

```python
tm.spline(xyz, s=3, k=2, nest=-1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
t = np.linspace(0, 1.75 * 2 * np.pi, 100)
x = np.sin(t)
y = np.cos(t)
z = t
x += rng.normal(scale=0.1, size=x.shape)
y += rng.normal(scale=0.1, size=y.shape)
z += rng.normal(scale=0.1, size=z.shape)
xyz = np.vstack((x, y, z)).T
tm.spline(xyz, s=3, k=2, nest=-1)
```

## Next Steps


---

*Source: test_metrics.py:11 | Complexity: Intermediate | Last updated: 2026-05-18*