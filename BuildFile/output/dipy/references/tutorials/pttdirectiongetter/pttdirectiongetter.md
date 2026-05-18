# How To: Pttdirectiongetter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test PTTDirectionGetter

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

### Step 1: Assign silly_model = SillyModel(...)

```python
silly_model = SillyModel(gtab=None)
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((3, 3, 3, 7))
```

### Step 3: Assign fit = silly_model.fit(...)

```python
fit = silly_model.fit(data)
```

### Step 4: Assign point = np.zeros(...)

```python
point = np.zeros(3)
```

### Step 5: Assign dir = unknown.copy(...)

```python
dir = unit_octahedron.vertices[0].copy()
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(dg.get_direction(point, dir), 1)
```

### Step 7: Assign pmf = np.zeros(...)

```python
pmf = np.zeros((3, 3, 3, unit_octahedron.theta.shape[0]))
```

### Step 8: Assign dg = PTTDirectionGetter.from_pmf(...)

```python
dg = PTTDirectionGetter.from_pmf(pmf, 90, unit_octahedron)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(dg.get_direction(point, dir), 1)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign dg = PTTDirectionGetter.from_shcoeff(...)

```python
dg = PTTDirectionGetter.from_shcoeff(fit.shm_coeff, 90, unit_octahedron)
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 13: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_length=0)
```

### Step 14: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_radius=-1)
```

### Step 15: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_quality=1)
```

### Step 16: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_count=0)
```

### Step 17: Assign coeff = np.zeros(...)

```python
coeff = np.zeros(data.shape[:-1] + (15,))
```


## Complete Example

```python
# Workflow
class SillyModel(SphHarmModel):

    def fit(self, data, mask=None):
        coeff = np.zeros(data.shape[:-1] + (15,))
        return SphHarmFit(self, coeff, mask=None)
silly_model = SillyModel(gtab=None)
data = np.zeros((3, 3, 3, 7))
fit = silly_model.fit(data)
point = np.zeros(3)
dir = unit_octahedron.vertices[0].copy()
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    dg = PTTDirectionGetter.from_shcoeff(fit.shm_coeff, 90, unit_octahedron)
npt.assert_equal(dg.get_direction(point, dir), 1)
pmf = np.zeros((3, 3, 3, unit_octahedron.theta.shape[0]))
dg = PTTDirectionGetter.from_pmf(pmf, 90, unit_octahedron)
npt.assert_equal(dg.get_direction(point, dir), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=tournier07_legacy_msg, category=PendingDeprecationWarning)
    npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_length=0)
    npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_radius=-1)
    npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_quality=1)
    npt.assert_raises(ValueError, PTTDirectionGetter.from_shcoeff, fit.shm_coeff, 90, unit_octahedron, basis_type='tournier07', probe_count=0)
```

## Next Steps


---

*Source: test_ptt_direction_getter.py:105 | Complexity: Advanced | Last updated: 2026-05-18*