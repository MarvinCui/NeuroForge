# How To: Particle Filtering Tracking Workflows

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dstack: test particle filtering tracking workflows

## Prerequisites

**Required Modules:**
- `os.path`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.image`
- `dipy.io.streamline`
- `dipy.reconst.shm`
- `dipy.testing`
- `dipy.workflows.mask`
- `dipy.workflows.reconst`
- `dipy.workflows.tracking`


## Step-by-Step Guide

### Step 1: Assign simple_gm = np.dstack(...)

```python
simple_gm = np.dstack([np.zeros(simple_gm.shape), np.zeros(simple_gm.shape), simple_gm, simple_gm, simple_gm, simple_gm, simple_gm, simple_gm, np.zeros(simple_gm.shape), np.zeros(simple_gm.shape)])
```


## Complete Example

```python
# Workflow
simple_gm = np.dstack([np.zeros(simple_gm.shape), np.zeros(simple_gm.shape), simple_gm, simple_gm, simple_gm, simple_gm, simple_gm, simple_gm, np.zeros(simple_gm.shape), np.zeros(simple_gm.shape)])
```

## Next Steps


---

*Source: test_tracking.py:70 | Complexity: Beginner | Last updated: 2026-05-18*