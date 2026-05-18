# How To: Change Slice

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test change_slice method in PeaksTab.

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

### Step 1: 'Test change_slice method in PeaksTab.'

```python
'Test change_slice method in PeaksTab.'
```

**Verification:**
```python
assert selected_slice.selected_value == 5
```

### Step 2: Assign tab = PeaksTab(...)

```python
tab = PeaksTab(peak_actor, 'Peaks 1', 'mock_peaks')
```

**Verification:**
```python
assert selected_slice.selected_value == 10
```

### Step 3: Call tab.build()

```python
tab.build(0)
```

### Step 4: Assign slider.value = 5

```python
slider.value = 5
```

### Step 5: Assign selected_slice = HorizonUIElement(...)

```python
selected_slice = HorizonUIElement(True, 0, None)
```

### Step 6: Assign tab._view_mode_toggler.obj.checked_labels = value

```python
tab._view_mode_toggler.obj.checked_labels = ['Cross section']
```

### Step 7: Call tab._change_slice()

```python
tab._change_slice(slider, selected_slice, sync_slice=True)
```

### Step 8: Call mock_sync.assert_not_called()

```python
mock_sync.assert_not_called()
```

**Verification:**
```python
assert selected_slice.selected_value == 5
```

### Step 9: Assign slider.value = 10

```python
slider.value = 10
```

### Step 10: Call tab._change_slice()

```python
tab._change_slice(slider, selected_slice)
```

### Step 11: Call mock_sync.assert_called_once()

```python
mock_sync.assert_called_once()
```

**Verification:**
```python
assert selected_slice.selected_value == 10
```


## Complete Example

```python
# Setup
# Fixtures: peak_actor, slider

# Workflow
'Test change_slice method in PeaksTab.'
tab = PeaksTab(peak_actor, 'Peaks 1', 'mock_peaks')
tab.build(0)
slider.value = 5
selected_slice = HorizonUIElement(True, 0, None)
tab._view_mode_toggler.obj.checked_labels = ['Cross section']
with patch.object(HorizonTab, 'on_slice_change') as mock_sync:
    tab._change_slice(slider, selected_slice, sync_slice=True)
    mock_sync.assert_not_called()
    assert selected_slice.selected_value == 5
    slider.value = 10
    tab._change_slice(slider, selected_slice)
    mock_sync.assert_called_once()
    assert selected_slice.selected_value == 10
```

## Next Steps


---

*Source: test_peak.py:205 | Complexity: Advanced | Last updated: 2026-05-18*