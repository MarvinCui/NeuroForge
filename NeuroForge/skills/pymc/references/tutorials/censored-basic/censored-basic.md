# How To: Censored Basic

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Configuration example: test censored basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.xtensor`
- `pytensor.xtensor.shape`
- `pytensor.xtensor.vectorization`
- `pymc.distributions`
- `pymc.dims`
- `pymc.model.core`
- `tests.dims.utils`

**Setup Required:**
```python
# Fixtures: lower, upper
```

## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'space': range(3), 'time': range(4)}
```


## Complete Example

```python
# Setup
# Fixtures: lower, upper

# Workflow
coords = {'space': range(3), 'time': range(4)}
```

## Next Steps


---

*Source: test_censored.py:33 | Complexity: Beginner | Last updated: 2026-05-18*