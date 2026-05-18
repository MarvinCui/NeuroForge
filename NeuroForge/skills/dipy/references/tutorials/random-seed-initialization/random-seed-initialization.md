# How To: Random Seed Initialization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the random generator can be initialized correctly with the
tracking seeds.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction`
- `dipy.reconst.csdeconv`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.local_tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test that the random generator can be initialized correctly with the\n    tracking seeds.\n    '

```python
'Test that the random generator can be initialized correctly with the\n    tracking seeds.\n    '
```

### Step 2: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(unit_octahedron)
```

### Step 3: Assign pmf = np.zeros(...)

```python
pmf = np.zeros((4, 4, 4, 3))
```

### Step 4: Assign x = np.array(...)

```python
x = np.array([0.0, 0, 0, 57.421434502602544])
```

### Step 5: Assign y = np.array(...)

```python
y = np.array([0.0, 1, 2, 21.566539227085478])
```

### Step 6: Assign z = np.array(...)

```python
z = np.array([1.0, 1, 1, 51.67881720942744])
```

### Step 7: Assign seeds = np.vstack(...)

```python
seeds = np.vstack([np.column_stack([x, y, z]), rng.random((10, 3))])
```

### Step 8: Assign sc = BinaryStoppingCriterion(...)

```python
sc = BinaryStoppingCriterion(np.ones((4, 4, 4)))
```

### Step 9: Assign dg = ProbabilisticDirectionGetter.from_pmf(...)

```python
dg = ProbabilisticDirectionGetter.from_pmf(pmf, 60, sphere)
```

### Step 10: Assign randoms_seeds = value

```python
randoms_seeds = [None, 0, 1, -1, np.iinfo(np.uint32).max + 1] + list(rng.random(10)) + list(rng.integers(0, np.iinfo(np.int32).max, 10))
```

### Step 11: Assign _ = Streamlines(...)

```python
_ = Streamlines(LocalTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, random_seed=rdm_seed))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test that the random generator can be initialized correctly with the\n    tracking seeds.\n    '
sphere = HemiSphere.from_sphere(unit_octahedron)
pmf = np.zeros((4, 4, 4, 3))
x = np.array([0.0, 0, 0, 57.421434502602544])
y = np.array([0.0, 1, 2, 21.566539227085478])
z = np.array([1.0, 1, 1, 51.67881720942744])
seeds = np.vstack([np.column_stack([x, y, z]), rng.random((10, 3))])
sc = BinaryStoppingCriterion(np.ones((4, 4, 4)))
dg = ProbabilisticDirectionGetter.from_pmf(pmf, 60, sphere)
randoms_seeds = [None, 0, 1, -1, np.iinfo(np.uint32).max + 1] + list(rng.random(10)) + list(rng.integers(0, np.iinfo(np.int32).max, 10))
for rdm_seed in randoms_seeds:
    _ = Streamlines(LocalTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, random_seed=rdm_seed))
```

## Next Steps


---

*Source: test_tracking.py:1161 | Complexity: Advanced | Last updated: 2026-05-18*