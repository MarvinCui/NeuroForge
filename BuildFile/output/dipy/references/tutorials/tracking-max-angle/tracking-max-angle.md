# How To: Tracking Max Angle

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests that the angle between streamline points is always smaller
then the input `max_angle` parameter.

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

### Step 1: 'This tests that the angle between streamline points is always smaller\n    then the input `max_angle` parameter.\n    '

```python
'This tests that the angle between streamline points is always smaller\n    then the input `max_angle` parameter.\n    '
```

### Step 2: Assign min_cos_sim = 1

```python
min_cos_sim = 1
```

### Step 3: Assign shape_img = value

```python
shape_img = [5, 5, 5]
```

### Step 4: Call shape_img.extend()

```python
shape_img.extend([sphere.vertices.shape[0]])
```

### Step 5: Assign mask = np.ones(...)

```python
mask = np.ones(shape_img[:3])
```

### Step 6: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 7: Assign random_pmf = rng.random(...)

```python
random_pmf = rng.random(shape_img)
```

### Step 8: Assign seeds = seeds_from_mask(...)

```python
seeds = seeds_from_mask(mask, affine, density=1)
```

### Step 9: Assign sc = ActStoppingCriterion.from_pve(...)

```python
sc = ActStoppingCriterion.from_pve(mask, np.zeros(shape_img[:3]), np.zeros(shape_img[:3]))
```

### Step 10: Assign max_angle = 20

```python
max_angle = 20
```

### Step 11: Assign step_size = 1

```python
step_size = 1
```

### Step 12: Assign dg = ProbabilisticDirectionGetter.from_pmf(...)

```python
dg = ProbabilisticDirectionGetter.from_pmf(random_pmf, max_angle, sphere, pmf_threshold=0.1)
```

### Step 13: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines(LocalTracking(dg, sc, seeds, affine, step_size))
```

### Step 14: Assign min_cos_sim = get_min_cos_similarity(...)

```python
min_cos_sim = get_min_cos_similarity(streamlines)
```

### Step 15: Call npt.assert_()

```python
npt.assert_(np.arccos(min_cos_sim) <= np.deg2rad(max_angle))
```

### Step 16: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines(ParticleFilteringTracking(dg, sc, seeds, affine, 1.0))
```

### Step 17: Assign min_cos_sim = get_min_cos_similarity(...)

```python
min_cos_sim = get_min_cos_similarity(streamlines)
```

### Step 18: Call npt.assert_()

```python
npt.assert_(np.arccos(min_cos_sim) <= np.deg2rad(max_angle))
```

### Step 19: Assign v = value

```python
v = sl[:-1] - sl[1:]
```

### Step 20: Assign cos_sim = np.dot(...)

```python
cos_sim = np.dot(v[i], v[i + 1])
```

### Step 21: Assign min_cos_sim = cos_sim

```python
min_cos_sim = cos_sim
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'This tests that the angle between streamline points is always smaller\n    then the input `max_angle` parameter.\n    '

def get_min_cos_similarity(streamlines):
    min_cos_sim = 1
    for sl in streamlines:
        if len(sl) > 1:
            v = sl[:-1] - sl[1:]
            for i in range(len(v) - 1):
                cos_sim = np.dot(v[i], v[i + 1])
                if cos_sim < min_cos_sim:
                    min_cos_sim = cos_sim
    return min_cos_sim
for sphere in [get_sphere(name='repulsion100'), HemiSphere.from_sphere(get_sphere(name='repulsion100'))]:
    shape_img = [5, 5, 5]
    shape_img.extend([sphere.vertices.shape[0]])
    mask = np.ones(shape_img[:3])
    affine = np.eye(4)
    random_pmf = rng.random(shape_img)
    seeds = seeds_from_mask(mask, affine, density=1)
    sc = ActStoppingCriterion.from_pve(mask, np.zeros(shape_img[:3]), np.zeros(shape_img[:3]))
    max_angle = 20
    step_size = 1
    dg = ProbabilisticDirectionGetter.from_pmf(random_pmf, max_angle, sphere, pmf_threshold=0.1)
    streamlines = Streamlines(LocalTracking(dg, sc, seeds, affine, step_size))
    min_cos_sim = get_min_cos_similarity(streamlines)
    npt.assert_(np.arccos(min_cos_sim) <= np.deg2rad(max_angle))
    streamlines = Streamlines(ParticleFilteringTracking(dg, sc, seeds, affine, 1.0))
    min_cos_sim = get_min_cos_similarity(streamlines)
    npt.assert_(np.arccos(min_cos_sim) <= np.deg2rad(max_angle))
```

## Next Steps


---

*Source: test_tracking.py:268 | Complexity: Advanced | Last updated: 2026-05-18*