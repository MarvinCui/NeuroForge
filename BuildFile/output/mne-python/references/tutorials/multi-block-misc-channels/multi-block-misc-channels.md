# How To: Multi Block Misc Channels

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test a file with many edge casses.

This file has multiple acquisition blocks, each tracking a different eye.
The coordinates are in raw units (not pixels or radians).
It has some misc channels (head position, saccade velocity, etc.)

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.eyelink._utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test a file with many edge casses.\n\n    This file has multiple acquisition blocks, each tracking a different eye.\n    The coordinates are in raw units (not pixels or radians).\n    It has some misc channels (head position, saccade velocity, etc.)\n    '

```python
'Test a file with many edge casses.\n\n    This file has multiple acquisition blocks, each tracking a different eye.\n    The coordinates are in raw units (not pixels or radians).\n    It has some misc channels (head position, saccade velocity, etc.)\n    '
```

**Verification:**
```python
assert raw.ch_names == chs_in_file
```

### Step 2: Assign out_file = value

```python
out_file = tmp_path / 'tmp_eyelink.asc'
```

**Verification:**
```python
assert raw.annotations.description[1] == 'SYNCTIME'
```

### Step 3: Call _simulate_eye_tracking_data()

```python
_simulate_eye_tracking_data(fname, out_file)
```

**Verification:**
```python
assert raw.annotations.description[-7] == 'BAD_ACQ_SKIP'
```

### Step 4: Assign chs_in_file = value

```python
chs_in_file = ['xpos_right', 'ypos_right', 'pupil_right', 'xvel_right', 'yvel_right', 'xres', 'yres', 'DIN', 'x_head', 'y_head', 'distance', 'xpos_left', 'ypos_left', 'pupil_left', 'xvel_left', 'yvel_left']
```

**Verification:**
```python
assert np.isclose(raw.annotations.onset[-7], 1.001)
```

### Step 5: Assign unknown = raw.get_data(...)

```python
data, times = raw.get_data(return_times=True)
```

**Verification:**
```python
assert np.isclose(raw.annotations.duration[-7], 0.1)
```

### Step 6: Assign button_idx = value

```python
button_idx = [ii for ii, desc in enumerate(raw.annotations.description) if 'button' in desc.lower()]
```

**Verification:**
```python
assert not np.isnan(data[0, np.where(times < 1)[0]]).any()
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw.annotations.onset[button_idx[0]], 2.102, atol=0.001)
```

**Verification:**
```python
assert np.isnan(data[0, np.logical_and(times > 1, times <= 1.1)]).all()
```

### Step 8: Call find_events()

```python
find_events(raw, verbose=True)
```

**Verification:**
```python
assert raw.annotations.description[-6] == 'button_1_press'
```

### Step 9: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(out_file, apply_offsets=True)
```

**Verification:**
```python
assert len(button_idx) == 6
```


## Complete Example

```python
# Setup
# Fixtures: fname, tmp_path

# Workflow
'Test a file with many edge casses.\n\n    This file has multiple acquisition blocks, each tracking a different eye.\n    The coordinates are in raw units (not pixels or radians).\n    It has some misc channels (head position, saccade velocity, etc.)\n    '
out_file = tmp_path / 'tmp_eyelink.asc'
_simulate_eye_tracking_data(fname, out_file)
with _record_warnings(), pytest.warns(RuntimeWarning, match='Raw eyegaze coordinates'), pytest.warns(RuntimeWarning, match='The eye being tracked changed'):
    raw = read_raw_eyelink(out_file, apply_offsets=True)
chs_in_file = ['xpos_right', 'ypos_right', 'pupil_right', 'xvel_right', 'yvel_right', 'xres', 'yres', 'DIN', 'x_head', 'y_head', 'distance', 'xpos_left', 'ypos_left', 'pupil_left', 'xvel_left', 'yvel_left']
assert raw.ch_names == chs_in_file
assert raw.annotations.description[1] == 'SYNCTIME'
assert raw.annotations.description[-7] == 'BAD_ACQ_SKIP'
assert np.isclose(raw.annotations.onset[-7], 1.001)
assert np.isclose(raw.annotations.duration[-7], 0.1)
data, times = raw.get_data(return_times=True)
assert not np.isnan(data[0, np.where(times < 1)[0]]).any()
assert np.isnan(data[0, np.logical_and(times > 1, times <= 1.1)]).all()
assert raw.annotations.description[-6] == 'button_1_press'
button_idx = [ii for ii, desc in enumerate(raw.annotations.description) if 'button' in desc.lower()]
assert len(button_idx) == 6
assert_allclose(raw.annotations.onset[button_idx[0]], 2.102, atol=0.001)
find_events(raw, verbose=True)
```

## Next Steps


---

*Source: test_eyelink.py:391 | Complexity: Advanced | Last updated: 2026-05-18*