# How To: Cmc Stopping Criterion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests that the cmc stopping criterion returns expected
streamline statuses.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.core.ndindex`
- `dipy.testing.decorators`
- `dipy.tracking.stopping_criterion`


## Step-by-Step Guide

### Step 1: 'This tests that the cmc stopping criterion returns expected\n    streamline statuses.\n    '

```python
'This tests that the cmc stopping criterion returns expected\n    streamline statuses.\n    '
```

### Step 2: Assign gm = np.array(...)

```python
gm = np.array([[[1, 1], [0, 0], [0, 0]]])
```

### Step 3: Assign wm = np.array(...)

```python
wm = np.array([[[0, 0], [1, 1], [0, 0]]])
```

### Step 4: Assign csf = np.array(...)

```python
csf = np.array([[[0, 0], [0, 0], [1, 1]]])
```

### Step 5: Assign include_map = gm

```python
include_map = gm
```

### Step 6: Assign exclude_map = csf

```python
exclude_map = csf
```

### Step 7: Assign cmc_tc = CmcStoppingCriterion(...)

```python
cmc_tc = CmcStoppingCriterion(include_map=include_map, exclude_map=exclude_map, step_size=1, average_voxel_size=1)
```

### Step 8: Assign cmc_tc_from_pve = CmcStoppingCriterion.from_pve(...)

```python
cmc_tc_from_pve = CmcStoppingCriterion.from_pve(wm_map=wm, gm_map=gm, csf_map=csf, step_size=1, average_voxel_size=1)
```

### Step 9: Assign outside_pts = value

```python
outside_pts = [[100, 100, 100], [0, -1, 1], [0, 10, 2], [0, 0.5, -0.51], [0, -0.51, 0.1]]
```

### Step 10: Assign idx = np.asarray(...)

```python
idx = np.asarray(idx, dtype='float64')
```

### Step 11: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(cmc_tc.get_include(idx), cmc_tc_from_pve.get_include(idx))
```

### Step 12: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(cmc_tc.get_exclude(idx), cmc_tc_from_pve.get_exclude(idx))
```

### Step 13: Assign pts = np.array(...)

```python
pts = np.array(ind, dtype='float64')
```

### Step 14: Assign state = cmc_tc.check_point(...)

```python
state = cmc_tc.check_point(pts)
```

### Step 15: Assign pts = np.array(...)

```python
pts = np.array(pts, dtype='float64')
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(cmc_tc.check_point(pts), int(StreamlineStatus.OUTSIDEIMAGE))
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(cmc_tc.get_exclude(pts), 0)
```

### Step 18: Call npt.assert_equal()

```python
npt.assert_equal(cmc_tc.get_include(pts), 0)
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.INVALIDPOINT))
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
```

### Step 21: Call npt.assert_equal()

```python
npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
```


## Complete Example

```python
# Workflow
'This tests that the cmc stopping criterion returns expected\n    streamline statuses.\n    '
gm = np.array([[[1, 1], [0, 0], [0, 0]]])
wm = np.array([[[0, 0], [1, 1], [0, 0]]])
csf = np.array([[[0, 0], [0, 0], [1, 1]]])
include_map = gm
exclude_map = csf
cmc_tc = CmcStoppingCriterion(include_map=include_map, exclude_map=exclude_map, step_size=1, average_voxel_size=1)
cmc_tc_from_pve = CmcStoppingCriterion.from_pve(wm_map=wm, gm_map=gm, csf_map=csf, step_size=1, average_voxel_size=1)
for idx in np.ndindex(wm.shape):
    idx = np.asarray(idx, dtype='float64')
    npt.assert_almost_equal(cmc_tc.get_include(idx), cmc_tc_from_pve.get_include(idx))
    npt.assert_almost_equal(cmc_tc.get_exclude(idx), cmc_tc_from_pve.get_exclude(idx))
for ind in ndindex(wm.shape):
    pts = np.array(ind, dtype='float64')
    state = cmc_tc.check_point(pts)
    if csf[ind] == 1:
        npt.assert_equal(state, int(StreamlineStatus.INVALIDPOINT))
    elif gm[ind] == 1:
        npt.assert_equal(state, int(StreamlineStatus.ENDPOINT))
    else:
        npt.assert_equal(state, int(StreamlineStatus.TRACKPOINT))
outside_pts = [[100, 100, 100], [0, -1, 1], [0, 10, 2], [0, 0.5, -0.51], [0, -0.51, 0.1]]
for pts in outside_pts:
    pts = np.array(pts, dtype='float64')
    npt.assert_equal(cmc_tc.check_point(pts), int(StreamlineStatus.OUTSIDEIMAGE))
    npt.assert_equal(cmc_tc.get_exclude(pts), 0)
    npt.assert_equal(cmc_tc.get_include(pts), 0)
```

## Next Steps


---

*Source: test_stopping_criterion.py:201 | Complexity: Advanced | Last updated: 2026-05-18*