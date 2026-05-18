# How To: Compare Events And Annotations

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: Test comparing annotations and events.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io.cnt`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: Assign events = np.array(...)

```python
events = np.array([[333, 0, 7], [1010, 0, 7], [1664, 0, 109], [2324, 0, 7], [2984, 0, 109]])
```


## Complete Example

```python
# Workflow
events = np.array([[333, 0, 7], [1010, 0, 7], [1664, 0, 109], [2324, 0, 7], [2984, 0, 109]])
```

## Next Steps


---

*Source: test_cnt.py:100 | Complexity: Beginner | Last updated: 2026-05-18*