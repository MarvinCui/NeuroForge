# How To: Dsi

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate sticks_and_ball: test dsi

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.dsi`
- `dipy.reconst.odf`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`


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

*Source: test_dsi_deconv.py:22 | Complexity: Beginner | Last updated: 2026-05-18*