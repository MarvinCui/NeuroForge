# How To: Vertex To Mni

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate array: Test conversion of vertices to MNI coordinates.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._freesurfer`
- `mne.datasets`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: Assign coords = np.array(...)

```python
coords = np.array([[-60.86, -11.18, -3.19], [-36.46, -93.18, -2.36], [-38.0, 50.08, -10.61], [47.14, 8.01, 46.93]])
```


## Complete Example

```python
# Workflow
coords = np.array([[-60.86, -11.18, -3.19], [-36.46, -93.18, -2.36], [-38.0, 50.08, -10.61], [47.14, 8.01, 46.93]])
```

## Next Steps


---

*Source: test_freesurfer.py:61 | Complexity: Beginner | Last updated: 2026-05-18*