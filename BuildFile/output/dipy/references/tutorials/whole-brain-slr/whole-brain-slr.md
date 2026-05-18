# How To: Whole Brain Slr

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate whole_brain_slr: test whole brain slr

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.streamlinear`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.tracking.distances`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign unknown = whole_brain_slr(...)

```python
moved, transform, qb_centroids1, qb_centroids2 = whole_brain_slr(f1, f2, x0='affine', verbose=True, rm_small_clusters=2, greater_than=0, less_than=np.inf, qbx_thr=[5, 2, 1], progressive=False)
```


## Complete Example

```python
# Workflow
moved, transform, qb_centroids1, qb_centroids2 = whole_brain_slr(f1, f2, x0='affine', verbose=True, rm_small_clusters=2, greater_than=0, less_than=np.inf, qbx_thr=[5, 2, 1], progressive=False)
```

## Next Steps


---

*Source: test_whole_brain_slr.py:29 | Complexity: Beginner | Last updated: 2026-05-18*