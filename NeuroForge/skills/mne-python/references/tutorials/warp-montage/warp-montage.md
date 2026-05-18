# How To: Warp Montage

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate compute_volume_registration: Test warping an montage based on intracranial electrode positions.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.preprocessing.ieeg`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: Assign unknown = compute_volume_registration(...)

```python
reg_affine, sdr_morph = compute_volume_registration(subject_brain, template_brain, zooms=zooms, niter=[3, 3, 3], pipeline=('translation', 'rigid', 'sdr'))
```


## Complete Example

```python
# Workflow
reg_affine, sdr_morph = compute_volume_registration(subject_brain, template_brain, zooms=zooms, niter=[3, 3, 3], pipeline=('translation', 'rigid', 'sdr'))
```

## Next Steps


---

*Source: test_volume.py:29 | Complexity: Beginner | Last updated: 2026-05-18*