# How To: Plot Calibration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting calibration data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `mne.datasets.testing`
- `calibration`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: fname, axes
```

## Step-by-Step Guide

### Step 1: 'Test plotting calibration data.'

```python
'Test plotting calibration data.'
```

**Verification:**
```python
assert ax.title.get_text() == f"Calibration ({cal_left['eye']} eye)"
```

### Step 2: Call plt.switch_backend()

```python
plt.switch_backend('agg')
```

**Verification:**
```python
assert len(ax.collections) == 2
```

### Step 3: Assign calibrations = read_eyelink_calibration(...)

```python
calibrations = read_eyelink_calibration(fname)
```

### Step 4: Assign cal_left = value

```python
cal_left = calibrations[0]
```

### Step 5: Assign fig = cal_left.plot(...)

```python
fig = cal_left.plot(show=True, show_offsets=True, axes=axes)
```

### Step 6: Assign ax = value

```python
ax = fig.axes[0]
```

### Step 7: Assign scatter1 = value

```python
scatter1 = ax.collections[0]
```

### Step 8: Assign scatter2 = value

```python
scatter2 = ax.collections[1]
```

### Step 9: Assign unknown = value

```python
px, py = cal_left['positions'].T
```

### Step 10: Assign unknown = value

```python
gaze_x, gaze_y = cal_left['gaze'].T
```

**Verification:**
```python
assert ax.title.get_text() == f"Calibration ({cal_left['eye']} eye)"
```

### Step 11: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(scatter1.get_offsets(), np.column_stack((px, py)))
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(scatter2.get_offsets(), np.column_stack((gaze_x, gaze_y)))
```

### Step 13: Call plt.close()

```python
plt.close(fig)
```

### Step 14: Assign axes = plt.subplot(...)

```python
axes = plt.subplot()
```


## Complete Example

```python
# Setup
# Fixtures: fname, axes

# Workflow
'Test plotting calibration data.'
import matplotlib.pyplot as plt
plt.switch_backend('agg')
if axes:
    axes = plt.subplot()
calibrations = read_eyelink_calibration(fname)
cal_left = calibrations[0]
fig = cal_left.plot(show=True, show_offsets=True, axes=axes)
ax = fig.axes[0]
scatter1 = ax.collections[0]
scatter2 = ax.collections[1]
px, py = cal_left['positions'].T
gaze_x, gaze_y = cal_left['gaze'].T
assert ax.title.get_text() == f"Calibration ({cal_left['eye']} eye)"
assert len(ax.collections) == 2
np.testing.assert_allclose(scatter1.get_offsets(), np.column_stack((px, py)))
np.testing.assert_allclose(scatter2.get_offsets(), np.column_stack((gaze_x, gaze_y)))
plt.close(fig)
```

## Next Steps


---

*Source: test_calibration.py:229 | Complexity: Advanced | Last updated: 2026-05-18*