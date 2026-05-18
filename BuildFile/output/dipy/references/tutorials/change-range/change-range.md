# How To: Change Range

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test change_range method in PeaksTab.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.viz.horizon.tab.base`
- `dipy.viz.horizon.tab.peak`
- `dipy.viz.horizon.visualizer.peak`

**Setup Required:**
```python
# Fixtures: peak_actor, slider
```

## Step-by-Step Guide

### Step 1: 'Test change_range method in PeaksTab.'

```python
'Test change_range method in PeaksTab.'
```

**Verification:**
```python
assert selected_range.selected_value == (10, 90)
```

### Step 2: Assign tab = PeaksTab(...)

```python
tab = PeaksTab(peak_actor, 'Peaks 1', 'mock_peaks')
```

### Step 3: Call tab.build()

```python
tab.build(0)
```

### Step 4: Assign slider.left_disk_value = 10

```python
slider.left_disk_value = 10
```

### Step 5: Assign slider.right_disk_value = 90

```python
slider.right_disk_value = 90
```

### Step 6: Assign selected_range = HorizonUIElement(...)

```python
selected_range = HorizonUIElement(True, (0, 0), None)
```

### Step 7: Call tab._change_range()

```python
tab._change_range(slider, selected_range)
```

**Verification:**
```python
assert selected_range.selected_value == (10, 90)
```


## Complete Example

```python
# Setup
# Fixtures: peak_actor, slider

# Workflow
'Test change_range method in PeaksTab.'
tab = PeaksTab(peak_actor, 'Peaks 1', 'mock_peaks')
tab.build(0)
slider.left_disk_value = 10
slider.right_disk_value = 90
selected_range = HorizonUIElement(True, (0, 0), None)
tab._change_range(slider, selected_range)
assert selected_range.selected_value == (10, 90)
```

## Next Steps


---

*Source: test_peak.py:190 | Complexity: Intermediate | Last updated: 2026-05-18*