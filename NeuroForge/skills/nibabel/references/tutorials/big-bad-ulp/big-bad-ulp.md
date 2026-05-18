# How To: Big Bad Ulp

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: test big bad ulp

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `numpy.testing`
- `arraywriters`
- `casting`
- `spatialimages`


## Step-by-Step Guide

### Step 1: Assign in_arr = np.array(...)

```python
in_arr = np.array([0, 0, 1, 2, 4, 5, -5, -np.inf, np.inf], dtype=ftype)
```


## Complete Example

```python
# Workflow
in_arr = np.array([0, 0, 1, 2, 4, 5, -5, -np.inf, np.inf], dtype=ftype)
```

## Next Steps


---

*Source: test_round_trip.py:82 | Complexity: Beginner | Last updated: 2026-05-18*