# How To: Ptt Tracking

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ptt tracking

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction`
- `dipy.io.image`
- `dipy.reconst.shm`
- `dipy.tracking.local_tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign unknown = get_fnames(...)

```python
fod_fname, seed_coordinates_fname, _ = get_fnames(name='ptt_minimal_dataset')
```

### Step 2: Assign unknown = load_nifti(...)

```python
fod, affine = load_nifti(fod_fname)
```

### Step 3: Assign seed_coordinates = value

```python
seed_coordinates = np.loadtxt(seed_coordinates_fname)[:10, :]
```

### Step 4: Assign sf = sh_to_sf(...)

```python
sf = sh_to_sf(fod, default_sphere, basis_type='tournier07', sh_order_max=8, legacy=False)
```

### Step 5: Assign unknown = 0

```python
sf[sf < 0] = 0
```

### Step 6: Assign sc = BinaryStoppingCriterion(...)

```python
sc = BinaryStoppingCriterion(np.ones(fod.shape[:3]))
```

### Step 7: Assign dg_default = PTTDirectionGetter.from_pmf(...)

```python
dg_default = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20)
```

### Step 8: Assign dg_count2 = PTTDirectionGetter.from_pmf(...)

```python
dg_count2 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_count=2, probe_radius=0.2)
```

### Step 9: Assign dg_quality10 = PTTDirectionGetter.from_pmf(...)

```python
dg_quality10 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_quality=10)
```

### Step 10: Assign dg_length2 = PTTDirectionGetter.from_pmf(...)

```python
dg_length2 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_length=2)
```

### Step 11: Assign dg = PTTDirectionGetter.from_pmf(...)

```python
dg = PTTDirectionGetter.from_pmf(np.zeros(sf.shape), sphere=default_sphere, max_angle=20)
```

### Step 12: Assign streamline_generator = LocalTracking(...)

```python
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine)
```

### Step 13: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines(streamline_generator)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(len(streamlines), 10)
```

### Step 15: Call npt.assert_()

```python
npt.assert_(np.all([len(s) == 1 for s in streamlines]))
```

### Step 16: Assign dg = PTTDirectionGetter.from_pmf(...)

```python
dg = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20)
```

### Step 17: Assign streamline_generator = LocalTracking(...)

```python
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine, maxlen=1, minlen=1)
```

### Step 18: Assign streams = Streamlines(...)

```python
streams = Streamlines(streamline_generator)
```

### Step 19: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.linalg.norm(streams[0][0] - streams[0][1]), 0.2, decimal=1)
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(len(streams), 10)
```

### Step 21: Call npt.assert_()

```python
npt.assert_(np.all([len(s) <= 3 for s in streams]))
```

### Step 22: Assign streamline_generator = LocalTracking(...)

```python
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine, maxlen=2, fixedstep=False)
```

### Step 23: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, Streamlines, streamline_generator)
```

### Step 24: Assign streamline_generator = LocalTracking(...)

```python
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine)
```

### Step 25: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines(streamline_generator)
```

### Step 26: Call npt.assert_equal()

```python
npt.assert_equal(len(streamlines), 10)
```

### Step 27: Call npt.assert_()

```python
npt.assert_(np.all([len(s) > 1 for s in streamlines]))
```


## Complete Example

```python
# Workflow
fod_fname, seed_coordinates_fname, _ = get_fnames(name='ptt_minimal_dataset')
fod, affine = load_nifti(fod_fname)
seed_coordinates = np.loadtxt(seed_coordinates_fname)[:10, :]
sf = sh_to_sf(fod, default_sphere, basis_type='tournier07', sh_order_max=8, legacy=False)
sf[sf < 0] = 0
sc = BinaryStoppingCriterion(np.ones(fod.shape[:3]))
dg_default = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20)
dg_count2 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_count=2, probe_radius=0.2)
dg_quality10 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_quality=10)
dg_length2 = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20, probe_length=2)
for dg in [dg_default, dg_count2, dg_quality10, dg_length2]:
    streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine)
    streamlines = Streamlines(streamline_generator)
    npt.assert_equal(len(streamlines), 10)
    npt.assert_(np.all([len(s) > 1 for s in streamlines]))
dg = PTTDirectionGetter.from_pmf(np.zeros(sf.shape), sphere=default_sphere, max_angle=20)
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine)
streamlines = Streamlines(streamline_generator)
npt.assert_equal(len(streamlines), 10)
npt.assert_(np.all([len(s) == 1 for s in streamlines]))
dg = PTTDirectionGetter.from_pmf(sf, sphere=default_sphere, max_angle=20)
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine, maxlen=1, minlen=1)
streams = Streamlines(streamline_generator)
npt.assert_almost_equal(np.linalg.norm(streams[0][0] - streams[0][1]), 0.2, decimal=1)
npt.assert_equal(len(streams), 10)
npt.assert_(np.all([len(s) <= 3 for s in streams]))
streamline_generator = LocalTracking(direction_getter=dg, step_size=0.2, stopping_criterion=sc, seeds=seed_coordinates, affine=affine, maxlen=2, fixedstep=False)
npt.assert_raises(ValueError, Streamlines, streamline_generator)
```

## Next Steps


---

*Source: test_ptt_direction_getter.py:24 | Complexity: Advanced | Last updated: 2026-05-18*