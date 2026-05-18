# How To: Calibration Newlines

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading a calibration with blank lines between each data line.

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
# Fixtures: fname, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading a calibration with blank lines between each data line.'

```python
'Test reading a calibration with blank lines between each data line.'
```

**Verification:**
```python
assert len(cals) == len(want_cals)
```

### Step 2: Assign want_cals = read_eyelink_calibration(...)

```python
want_cals = read_eyelink_calibration(fname)
```

**Verification:**
```python
assert cals[1]['eye'] == want_cals[1]['eye']
```

### Step 3: Assign lines = Path.read_text.splitlines(...)

```python
lines = Path(fname).read_text().splitlines()
```

### Step 4: Assign cal_start = lines.index(...)

```python
cal_start = lines.index('>>>>>>> CALIBRATION (HV13,P-CR) FOR LEFT: <<<<<<<<<')
```

### Step 5: Assign cal_end = lines.index(...)

```python
cal_end = lines.index('INPUT\t5509657\t0')
```

### Step 6: Assign cal_block = value

```python
cal_block = lines[cal_start:cal_end + 1]
```

### Step 7: Assign interleaved = value

```python
interleaved = [elem for line in cal_block for elem in (line, '')]
```

### Step 8: Assign new_lines = value

```python
new_lines = lines[:cal_start] + interleaved + lines[cal_end + 1:]
```

### Step 9: Assign out_fname = value

```python
out_fname = tmp_path / 'weird_calibration.asc'
```

### Step 10: Call out_fname.write_text()

```python
out_fname.write_text('\n'.join(new_lines))
```

### Step 11: Assign cals = read_eyelink_calibration(...)

```python
cals = read_eyelink_calibration(out_fname)
```

**Verification:**
```python
assert len(cals) == len(want_cals)
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(cals[0]['onset'], want_cals[0]['onset'])
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(cals[0]['positions'], want_cals[0]['positions'])
```

### Step 14: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(cals[1]['offsets'], want_cals[1]['offsets'])
```

### Step 15: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(cals[0]['gaze'], want_cals[0]['gaze'])
```


## Complete Example

```python
# Setup
# Fixtures: fname, tmp_path

# Workflow
'Test reading a calibration with blank lines between each data line.'
want_cals = read_eyelink_calibration(fname)
lines = Path(fname).read_text().splitlines()
cal_start = lines.index('>>>>>>> CALIBRATION (HV13,P-CR) FOR LEFT: <<<<<<<<<')
cal_end = lines.index('INPUT\t5509657\t0')
cal_block = lines[cal_start:cal_end + 1]
interleaved = [elem for line in cal_block for elem in (line, '')]
new_lines = lines[:cal_start] + interleaved + lines[cal_end + 1:]
out_fname = tmp_path / 'weird_calibration.asc'
out_fname.write_text('\n'.join(new_lines))
cals = read_eyelink_calibration(out_fname)
assert len(cals) == len(want_cals)
assert cals[1]['eye'] == want_cals[1]['eye']
np.testing.assert_allclose(cals[0]['onset'], want_cals[0]['onset'])
np.testing.assert_allclose(cals[0]['positions'], want_cals[0]['positions'])
np.testing.assert_allclose(cals[1]['offsets'], want_cals[1]['offsets'])
np.testing.assert_allclose(cals[0]['gaze'], want_cals[0]['gaze'])
```

## Next Steps


---

*Source: test_calibration.py:260 | Complexity: Advanced | Last updated: 2026-05-18*