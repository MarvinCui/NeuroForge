# How To: Slice Viz

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: mock, pytest

## Overview

Instantiate array: Fixture to create a Slice Actors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.viz.horizon.tab.base`
- `dipy.viz.horizon.tab.slice`
- `dipy.viz.horizon.visualizer.slice`

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

*Source: test_slices.py:22 | Complexity: Beginner | Last updated: 2026-05-18*