# How To: Data Complete Mask

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: Test for a special case due to matplotlib 2.1.0.

When the data is completely masked, then we have plotting issues
See similar issue #9280 reported in matplotlib. This function
tests the patch added for this particular issue.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn.conftest`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays._slicers`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays._utils`

**Setup Required:**
```python
# Fixtures: affine_eye, display
```

## Step-by-Step Guide

### Step 1: 'Test for a special case due to matplotlib 2.1.0.\n\n    When the data is completely masked, then we have plotting issues\n    See similar issue #9280 reported in matplotlib. This function\n    tests the patch added for this particular issue.\n    '

```python
'Test for a special case due to matplotlib 2.1.0.\n\n    When the data is completely masked, then we have plotting issues\n    See similar issue #9280 reported in matplotlib. This function\n    tests the patch added for this particular issue.\n    '
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros((10, 20, 30))
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign n_cuts = value

```python
n_cuts = 3 if display == OrthoSlicer else 4
```

### Step 5: Assign display = display(...)

```python
display = display(cut_coords=(0,) * n_cuts)
```

### Step 6: Call display.add_overlay()

```python
display.add_overlay(img)
```

### Step 7: Call display.close()

```python
display.close()
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, display

# Workflow
'Test for a special case due to matplotlib 2.1.0.\n\n    When the data is completely masked, then we have plotting issues\n    See similar issue #9280 reported in matplotlib. This function\n    tests the patch added for this particular issue.\n    '
data = np.zeros((10, 20, 30))
img = Nifti1Image(data, affine_eye)
n_cuts = 3 if display == OrthoSlicer else 4
display = display(cut_coords=(0,) * n_cuts)
display.add_overlay(img)
display.close()
```

## Next Steps


---

*Source: test_displays.py:344 | Complexity: Intermediate | Last updated: 2026-05-18*