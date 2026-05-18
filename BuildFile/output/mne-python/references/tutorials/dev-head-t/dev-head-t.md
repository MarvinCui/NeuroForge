# How To: Dev Head T

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate array: Test dev_head_t computation for Artemis123.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.artemis123.utils`
- `mne.io.tests.test_raw`
- `mne.utils._testing`


## Step-by-Step Guide

### Step 1: Assign dev_head_t_2 = np.array(...)

```python
dev_head_t_2 = np.array([[0.989, 0.1475, -0.00809, 0.0004997], [-0.1476, 0.9846, -0.09389, 0.001962], [-0.005888, 0.09406, 0.9955, -0.0161], [0.0, 0.0, 0.0, 1.0]])
```


## Complete Example

```python
# Workflow
dev_head_t_2 = np.array([[0.989, 0.1475, -0.00809, 0.0004997], [-0.1476, 0.9846, -0.09389, 0.001962], [-0.005888, 0.09406, 0.9955, -0.0161], [0.0, 0.0, 0.0, 1.0]])
```

## Next Steps


---

*Source: test_artemis123.py:68 | Complexity: Beginner | Last updated: 2026-05-18*