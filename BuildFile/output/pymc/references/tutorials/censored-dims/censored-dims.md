# How To: Censored Dims

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: Test that both censored (and the underlying dist) have all the implied and explicit dims.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'a': range(3), 'b': range(4), 'c': range(5), 'd': range(6)}
```


## Complete Example

```python
# Workflow
coords = {'a': range(3), 'b': range(4), 'c': range(5), 'd': range(6)}
```

## Next Steps


---

*Source: test_censored.py:51 | Complexity: Beginner | Last updated: 2026-05-18*