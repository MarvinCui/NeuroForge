# How To: Read Calibration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading calibration data from an eyelink asc file.

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
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test reading calibration data from an eyelink asc file.'

```python
'Test reading calibration data from an eyelink asc file.'
```

**Verification:**
```python
assert len(calibrations) == 2
```

### Step 2: Assign calibrations = read_eyelink_calibration(...)

```python
calibrations = read_eyelink_calibration(fname)
```

**Verification:**
```python
assert calibrations[0]['model'] == 'HV13'
```

### Step 3: Assign POSITIONS_L = value

```python
POSITIONS_L = ([960, 540], [960, 92], [960, 987], [115, 540], [1804, 540], [216, 145], [1703, 145], [216, 934], [1703, 934], [537, 316], [1382, 316], [537, 763], [1382, 763])
```

**Verification:**
```python
assert calibrations[1]['model'] == 'HV13'
```

### Step 4: Assign DIFF_L = value

```python
DIFF_L = ([9.9, -4.1], [-7.8, 16.0], [-1.9, -14.2], [13.5, -14.8], [8.1, 1.0], [-7.0, -15.4], [-10.1, -1.4], [-0.3, 6.9], [-32.3, -28.1], [8.2, 7.6], [9.6, 2.1], [-10.6, -2.0], [-11.8, 8.4])
```

**Verification:**
```python
assert calibrations[0]['eye'] == 'left'
```

### Step 5: Assign GAZE_L = value

```python
GAZE_L = np.array(POSITIONS_L) + np.array(DIFF_L)
```

**Verification:**
```python
assert calibrations[1]['eye'] == 'right'
```

### Step 6: Assign POSITIONS_R = value

```python
POSITIONS_R = ([960, 540], [960, 92], [960, 987], [115, 540], [1804, 540], [216, 145], [1703, 145], [216, 934], [1703, 934], [537, 316], [1382, 316], [537, 763], [1382, 763])
```

**Verification:**
```python
assert calibrations[0]['avg_error'] == 0.3
```

### Step 7: Assign DIFF_R = value

```python
DIFF_R = ([-5.2, -16.1], [23.7, 1.3], [2.0, -9.3], [4.4, 1.5], [-6.5, -12.7], [16.6, -7.5], [5.7, -1.8], [15.4, -3.5], [-2.0, -10.2], [0.1, 8.3], [1.9, -15.8], [-24.8, -2.3], [3.2, -9.2])
```

**Verification:**
```python
assert calibrations[0]['max_error'] == 0.9
```

### Step 8: Assign GAZE_R = value

```python
GAZE_R = np.array(POSITIONS_R) + np.array(DIFF_R)
```

**Verification:**
```python
assert calibrations[1]['avg_error'] == 0.31
```

### Step 9: Assign OFFSETS_R = value

```python
OFFSETS_R = [0.36, 0.5, 0.2, 0.1, 0.3, 0.38, 0.13, 0.33, 0.22, 0.18, 0.34, 0.52, 0.21]
```

**Verification:**
```python
assert calibrations[1]['max_error'] == 0.52
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(calibrations[0]['onset'], -6.85)
```

### Step 11: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(calibrations[1]['onset'], -6.85)
```

**Verification:**
```python
assert calibrations[0]['model'] == 'HV13'
```

### Step 12: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(POSITIONS_L, calibrations[0]['positions'])
```

### Step 13: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(POSITIONS_R, calibrations[1]['positions'])
```

### Step 14: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(GAZE_L, calibrations[0]['gaze'])
```

### Step 15: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(GAZE_R, calibrations[1]['gaze'])
```

### Step 16: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(OFFSETS_R, calibrations[1]['offsets'])
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test reading calibration data from an eyelink asc file.'
calibrations = read_eyelink_calibration(fname)
POSITIONS_L = ([960, 540], [960, 92], [960, 987], [115, 540], [1804, 540], [216, 145], [1703, 145], [216, 934], [1703, 934], [537, 316], [1382, 316], [537, 763], [1382, 763])
DIFF_L = ([9.9, -4.1], [-7.8, 16.0], [-1.9, -14.2], [13.5, -14.8], [8.1, 1.0], [-7.0, -15.4], [-10.1, -1.4], [-0.3, 6.9], [-32.3, -28.1], [8.2, 7.6], [9.6, 2.1], [-10.6, -2.0], [-11.8, 8.4])
GAZE_L = np.array(POSITIONS_L) + np.array(DIFF_L)
POSITIONS_R = ([960, 540], [960, 92], [960, 987], [115, 540], [1804, 540], [216, 145], [1703, 145], [216, 934], [1703, 934], [537, 316], [1382, 316], [537, 763], [1382, 763])
DIFF_R = ([-5.2, -16.1], [23.7, 1.3], [2.0, -9.3], [4.4, 1.5], [-6.5, -12.7], [16.6, -7.5], [5.7, -1.8], [15.4, -3.5], [-2.0, -10.2], [0.1, 8.3], [1.9, -15.8], [-24.8, -2.3], [3.2, -9.2])
GAZE_R = np.array(POSITIONS_R) + np.array(DIFF_R)
OFFSETS_R = [0.36, 0.5, 0.2, 0.1, 0.3, 0.38, 0.13, 0.33, 0.22, 0.18, 0.34, 0.52, 0.21]
assert len(calibrations) == 2
np.testing.assert_allclose(calibrations[0]['onset'], -6.85)
np.testing.assert_allclose(calibrations[1]['onset'], -6.85)
assert calibrations[0]['model'] == 'HV13'
assert calibrations[1]['model'] == 'HV13'
assert calibrations[0]['eye'] == 'left'
assert calibrations[1]['eye'] == 'right'
assert calibrations[0]['avg_error'] == 0.3
assert calibrations[0]['max_error'] == 0.9
assert calibrations[1]['avg_error'] == 0.31
assert calibrations[1]['max_error'] == 0.52
np.testing.assert_array_equal(POSITIONS_L, calibrations[0]['positions'])
np.testing.assert_array_equal(POSITIONS_R, calibrations[1]['positions'])
np.testing.assert_array_equal(GAZE_L, calibrations[0]['gaze'])
np.testing.assert_array_equal(GAZE_R, calibrations[1]['gaze'])
np.testing.assert_array_equal(OFFSETS_R, calibrations[1]['offsets'])
```

## Next Steps


---

*Source: test_calibration.py:121 | Complexity: Advanced | Last updated: 2026-05-18*