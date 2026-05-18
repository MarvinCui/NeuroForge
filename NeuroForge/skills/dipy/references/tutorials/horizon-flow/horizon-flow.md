# How To: Horizon Flow

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate array: test horizon flow

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.io.utils`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `dipy.viz.horizon.app`
- `dipy.workflows.viz`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign affine = np.array(...)

```python
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```

## Next Steps


---

*Source: test_viz.py:43 | Complexity: Beginner | Last updated: 2026-05-18*