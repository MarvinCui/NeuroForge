# How To: Data

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate meshgrid: data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `arviz`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.spatial`
- `pymc`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = np.meshgrid(...)

```python
x1, x2, x3 = np.meshgrid(np.linspace(0, 10, 5), np.linspace(20, 30, 5), np.linspace(10, 20, 5))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
x1, x2, x3 = np.meshgrid(np.linspace(0, 10, 5), np.linspace(20, 30, 5), np.linspace(10, 20, 5))
```

## Next Steps


---

*Source: test_hsgp_approx.py:89 | Complexity: Beginner | Last updated: 2026-05-18*