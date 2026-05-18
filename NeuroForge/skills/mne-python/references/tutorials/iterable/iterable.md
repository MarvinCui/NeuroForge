# How To: Iterable

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate setup_volume_source_space: Test iterable support for simulate_raw.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.chpi`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.simulation`
- `mne.simulation.source`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.tests.test_chpi`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(pos=dict(rr=[[-0.05, 0, 0], [0.1, 0, 0]], nn=[[0, 1.0, 0], [0, 1.0, 0]]))
```


## Complete Example

```python
# Workflow
src = setup_volume_source_space(pos=dict(rr=[[-0.05, 0, 0], [0.1, 0, 0]], nn=[[0, 1.0, 0], [0, 1.0, 0]]))
```

## Next Steps


---

*Source: test_raw.py:91 | Complexity: Beginner | Last updated: 2026-05-18*