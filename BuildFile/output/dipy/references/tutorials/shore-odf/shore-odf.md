# How To: Shore Odf

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate sticks_and_ball: test shore odf

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.reconst.shore`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign unknown = sticks_and_ball(...)

```python
data, golden_directions = sticks_and_ball(gtab, d=0.0015, S0=100, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=None)
```


## Complete Example

```python
# Workflow
data, golden_directions = sticks_and_ball(gtab, d=0.0015, S0=100, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=None)
```

## Next Steps


---

*Source: test_shore_odf.py:26 | Complexity: Beginner | Last updated: 2026-05-18*