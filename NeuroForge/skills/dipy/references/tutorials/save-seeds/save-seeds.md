# How To: Save Seeds

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test save seeds

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign tissue = np.array(...)

```python
tissue = np.array([[2, 1, 1, 2, 1], [2, 2, 1, 1, 2], [1, 1, 1, 1, 1], [1, 1, 1, 2, 2], [0, 1, 1, 1, 2], [0, 1, 1, 0, 2], [1, 0, 1, 1, 1]])
```

### Step 2: Assign tissue = value

```python
tissue = tissue[None]
```

### Step 3: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(unit_octahedron)
```

### Step 4: Assign pmf_lookup = np.array(...)

```python
pmf_lookup = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 1.0]])
```

### Step 5: Assign pmf = value

```python
pmf = pmf_lookup[(tissue > 0).astype('int')]
```

### Step 6: Assign x = np.array(...)

```python
x = np.array([0.0, 0, 0, 0, 0, 0, 0])
```

### Step 7: Assign y = np.array(...)

```python
y = np.array([0.0, 1, 2, 3, 4, 5, 6])
```

### Step 8: Assign z = np.array(...)

```python
z = np.array([1.0, 1, 1, 0, 1, 1, 1])
```

### Step 9: Assign seeds = np.column_stack(...)

```python
seeds = np.column_stack([x, y, z])
```

### Step 10: Assign endpoint_mask = value

```python
endpoint_mask = tissue == StreamlineStatus.ENDPOINT
```

### Step 11: Assign invalidpoint_mask = value

```python
invalidpoint_mask = tissue == StreamlineStatus.INVALIDPOINT
```

### Step 12: Assign sc = ActStoppingCriterion(...)

```python
sc = ActStoppingCriterion(endpoint_mask, invalidpoint_mask)
```

### Step 13: Assign dg = ProbabilisticDirectionGetter.from_pmf(...)

```python
dg = ProbabilisticDirectionGetter.from_pmf(pmf, 60, sphere)
```

### Step 14: Assign streamlines_generator = LocalTracking(...)

```python
streamlines_generator = LocalTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, return_all=False, save_seeds=True)
```

### Step 15: Assign streamlines_not_all = iter(...)

```python
streamlines_not_all = iter(streamlines_generator)
```

### Step 16: Assign unknown = next(...)

```python
_, seed = next(streamlines_not_all)
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(seed, seeds[0])
```

### Step 18: Assign unknown = next(...)

```python
_, seed = next(streamlines_not_all)
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(seed, seeds[1])
```

### Step 20: Assign pft_streamlines = ParticleFilteringTracking(...)

```python
pft_streamlines = ParticleFilteringTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, max_cross=1, return_all=False, save_seeds=True)
```

### Step 21: Assign streamlines = iter(...)

```python
streamlines = iter(pft_streamlines)
```

### Step 22: Assign unknown = next(...)

```python
_, seed = next(streamlines)
```

### Step 23: Call npt.assert_equal()

```python
npt.assert_equal(seed, seeds[0])
```

### Step 24: Assign unknown = next(...)

```python
_, seed = next(streamlines)
```

### Step 25: Call npt.assert_equal()

```python
npt.assert_equal(seed, seeds[1])
```


## Complete Example

```python
# Workflow
tissue = np.array([[2, 1, 1, 2, 1], [2, 2, 1, 1, 2], [1, 1, 1, 1, 1], [1, 1, 1, 2, 2], [0, 1, 1, 1, 2], [0, 1, 1, 0, 2], [1, 0, 1, 1, 1]])
tissue = tissue[None]
sphere = HemiSphere.from_sphere(unit_octahedron)
pmf_lookup = np.array([[0.0, 0.0, 0.0], [0.0, 0.0, 1.0]])
pmf = pmf_lookup[(tissue > 0).astype('int')]
x = np.array([0.0, 0, 0, 0, 0, 0, 0])
y = np.array([0.0, 1, 2, 3, 4, 5, 6])
z = np.array([1.0, 1, 1, 0, 1, 1, 1])
seeds = np.column_stack([x, y, z])
endpoint_mask = tissue == StreamlineStatus.ENDPOINT
invalidpoint_mask = tissue == StreamlineStatus.INVALIDPOINT
sc = ActStoppingCriterion(endpoint_mask, invalidpoint_mask)
dg = ProbabilisticDirectionGetter.from_pmf(pmf, 60, sphere)
streamlines_generator = LocalTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, return_all=False, save_seeds=True)
streamlines_not_all = iter(streamlines_generator)
_, seed = next(streamlines_not_all)
npt.assert_equal(seed, seeds[0])
_, seed = next(streamlines_not_all)
npt.assert_equal(seed, seeds[1])
pft_streamlines = ParticleFilteringTracking(direction_getter=dg, stopping_criterion=sc, seeds=seeds, affine=np.eye(4), step_size=1.0, max_cross=1, return_all=False, save_seeds=True)
streamlines = iter(pft_streamlines)
_, seed = next(streamlines)
npt.assert_equal(seed, seeds[0])
_, seed = next(streamlines)
npt.assert_equal(seed, seeds[1])
```

## Next Steps


---

*Source: test_tracking.py:193 | Complexity: Advanced | Last updated: 2026-05-18*