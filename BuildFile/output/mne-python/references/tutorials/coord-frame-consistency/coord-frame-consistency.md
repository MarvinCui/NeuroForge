# How To: Coord Frame Consistency

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test consistency between coord frame mappings.

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `shutil`
- `zipfile`
- `numpy`
- `pooch`
- `pytest`
- `mne._fiff.constants`
- `mne.forward._make_forward`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test consistency between coord frame mappings.'

```python
'Test consistency between coord frame mappings.'
```

**Verification:**
```python
assert ignore_frames.issubset(all_frames)
```

### Step 2: Assign all_frames = set(...)

```python
all_frames = set((key for key in dir(FIFF) if key.startswith(('FIFFV_COORD_', 'FIFFV_MNE_COORD'))))
```

**Verification:**
```python
assert set(_frame_to_str) == all_ints
```

### Step 3: Assign ignore_frames = set(...)

```python
ignore_frames = set((f'FIFFV_COORD_{name}' for name in '\n        MRI_SLICE MRI_DISPLAY DICOM_DEVICE IMAGING_DEVICE\n        '.strip().split()))
```

**Verification:**
```python
assert set(_verbose_frames) == all_ints
```

### Step 4: Assign all_ints = set(...)

```python
all_ints = set((FIFF[key] for key in all_frames))
```

**Verification:**
```python
assert set(_coord_frame_named) == all_ints
```


## Complete Example

```python
# Workflow
'Test consistency between coord frame mappings.'
all_frames = set((key for key in dir(FIFF) if key.startswith(('FIFFV_COORD_', 'FIFFV_MNE_COORD'))))
ignore_frames = set((f'FIFFV_COORD_{name}' for name in '\n        MRI_SLICE MRI_DISPLAY DICOM_DEVICE IMAGING_DEVICE\n        '.strip().split()))
ignore_frames |= set((f'FIFFV_MNE_COORD_{name}' for name in '\n        DIGITIZER TUFTS_EEG FS_TAL_GTZ FS_TAL_LTZ\n        '.strip().split()))
assert ignore_frames.issubset(all_frames)
all_frames -= ignore_frames
all_ints = set((FIFF[key] for key in all_frames))
assert set(_frame_to_str) == all_ints
assert set(_verbose_frames) == all_ints
assert set(_coord_frame_named) == all_ints
```

## Next Steps


---

*Source: test_constants.py:434 | Complexity: Intermediate | Last updated: 2026-05-18*