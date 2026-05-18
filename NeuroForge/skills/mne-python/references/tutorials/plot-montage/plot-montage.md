# How To: Plot Montage

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate make_dig_montage: Test plotting montages.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.io`


## Step-by-Step Guide

### Step 1: Assign montage = make_dig_montage(...)

```python
montage = make_dig_montage(nasion=[1, 1, 1], lpa=[2, 2, 2], rpa=[3, 3, 3], hsp=np.full((N_HSP, 3), 4), hpi=np.full((N_HPI, 3), 4), coord_frame='head')
```


## Complete Example

```python
# Workflow
montage = make_dig_montage(nasion=[1, 1, 1], lpa=[2, 2, 2], rpa=[3, 3, 3], hsp=np.full((N_HSP, 3), 4), hpi=np.full((N_HPI, 3), 4), coord_frame='head')
```

## Next Steps


---

*Source: test_montage.py:42 | Complexity: Beginner | Last updated: 2026-05-18*