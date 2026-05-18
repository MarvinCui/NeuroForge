# How To: Horizon Events

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate array: test horizon events

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.stateful_tractogram`
- `dipy.io.utils`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `fury`
- `dipy.viz.horizon.app`
- `dipy.segment.tests.test_bundles`
- `dipy.segment.tests.test_bundles`
- `dipy.viz`

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

*Source: test_apps.py:34 | Complexity: Beginner | Last updated: 2026-05-18*