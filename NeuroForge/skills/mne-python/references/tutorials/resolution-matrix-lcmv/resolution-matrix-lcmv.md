# How To: Resolution Matrix Lcmv

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate make_lcmv: Test computation of resolution matrix for LCMV beamformers.

## Prerequisites

**Required Modules:**
- `copy`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.beamformer`
- `mne.datasets`


## Step-by-Step Guide

### Step 1: Assign filters = make_lcmv(...)

```python
filters = make_lcmv(info, forward_fxd, data_cov, reg=0.0, noise_cov=noise_cov, pick_ori=None, rank=None, weight_norm=None, reduce_rank=False, verbose=False)
```


## Complete Example

```python
# Workflow
filters = make_lcmv(info, forward_fxd, data_cov, reg=0.0, noise_cov=noise_cov, pick_ori=None, rank=None, weight_norm=None, reduce_rank=False, verbose=False)
```

## Next Steps


---

*Source: test_resolution_matrix.py:58 | Complexity: Beginner | Last updated: 2026-05-18*