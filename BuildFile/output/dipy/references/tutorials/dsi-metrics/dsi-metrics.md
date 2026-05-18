# How To: Dsi Metrics

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate multi_tensor: test dsi metrics

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.reconst.dsi`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign unknown = multi_tensor(...)

```python
S_1, _ = multi_tensor(gtab, mevals * 2.0, S0=100, angles=[(0, 0), (60, 0)], fractions=[50, 50], snr=None)
```


## Complete Example

```python
# Workflow
S_1, _ = multi_tensor(gtab, mevals * 2.0, S0=100, angles=[(0, 0), (60, 0)], fractions=[50, 50], snr=None)
```

## Next Steps


---

*Source: test_dsi_metrics.py:27 | Complexity: Beginner | Last updated: 2026-05-18*