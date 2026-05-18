# How To: Get Connectome

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate asarray: test get connectome

## Prerequisites

**Required Modules:**
- `json`
- `numpy`
- `pytest`
- `nilearn.plotting`
- `nilearn.plotting.js_plotting_utils`
- `nilearn.plotting.tests.test_js_plotting_utils`


## Step-by-Step Guide

### Step 1: Assign expected_x = np.asarray(...)

```python
expected_x = np.asarray([0, 0, 0, 0, 20, 0, 10, 10, 0, 10, 30, 0, 20, 0, 0, 20, 20, 0, 20, 40, 0, 30, 10, 0, 30, 30, 0, 40, 20, 0, 40, 40, 0], dtype='<f4')
```


## Complete Example

```python
# Workflow
expected_x = np.asarray([0, 0, 0, 0, 20, 0, 10, 10, 0, 10, 30, 0, 20, 0, 0, 20, 20, 0, 20, 40, 0, 30, 10, 0, 30, 30, 0, 40, 20, 0, 40, 40, 0], dtype='<f4')
```

## Next Steps


---

*Source: test_html_connectome.py:53 | Complexity: Beginner | Last updated: 2026-05-18*