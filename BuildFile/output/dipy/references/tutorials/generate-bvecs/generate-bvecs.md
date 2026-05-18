# How To: Generate Bvecs

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests whether we have properly generated bvecs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Tests whether we have properly generated bvecs.'

```python
'Tests whether we have properly generated bvecs.'
```

### Step 2: Assign bvecs = generate_bvecs(...)

```python
bvecs = generate_bvecs(100, rng=rng)
```

### Step 3: Assign norm = value

```python
norm = [np.linalg.norm(v) for v in bvecs]
```

### Step 4: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(norm, np.ones(100))
```

### Step 5: Assign bvecs_2 = generate_bvecs(...)

```python
bvecs_2 = generate_bvecs(2, rng=rng)
```

### Step 6: Assign cos_theta = np.dot(...)

```python
cos_theta = np.dot(bvecs_2[0], bvecs_2[1])
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(cos_theta, 0.0, decimal=6)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Tests whether we have properly generated bvecs.'
bvecs = generate_bvecs(100, rng=rng)
norm = [np.linalg.norm(v) for v in bvecs]
npt.assert_almost_equal(norm, np.ones(100))
bvecs_2 = generate_bvecs(2, rng=rng)
cos_theta = np.dot(bvecs_2[0], bvecs_2[1])
npt.assert_almost_equal(cos_theta, 0.0, decimal=6)
```

## Next Steps


---

*Source: test_gradients.py:519 | Complexity: Intermediate | Last updated: 2026-05-18*