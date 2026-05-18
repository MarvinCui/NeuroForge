# How To: Annotations Without Offset

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test read of annotations without offset.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test read of annotations without offset.'

```python
'Test read of annotations without offset.'
```

**Verification:**
```python
assert raw.annotations[-1]['description'] == 'test string'
```

### Step 2: Assign out_file = value

```python
out_file = tmp_path / 'tmp_eyelink.asc'
```

**Verification:**
```python
assert raw.annotations[1]['description'] == '-2 SYNCTIME'
```

### Step 3: Assign ts = value

```python
ts = lines[-3].split('\t')[0]
```

**Verification:**
```python
assert raw.annotations[-1]['description'] == 'test string'
```

### Step 4: Assign line = value

```python
line = f'MSG\t{ts} test string\n'
```

**Verification:**
```python
assert raw.annotations[1]['description'] == 'SYNCTIME'
```

### Step 5: Assign lines = value

```python
lines = lines[:-3] + [line] + lines[-3:]
```

**Verification:**
```python
assert_allclose(raw.annotations[-1]['onset'], onset1)
```

### Step 6: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(out_file, apply_offsets=False)
```

**Verification:**
```python
assert_allclose(raw.annotations[1]['onset'], onset2 - 2 / raw.info['sfreq'])
```

### Step 7: Assign onset1 = value

```python
onset1 = raw.annotations[-1]['onset']
```

**Verification:**
```python
assert raw.annotations[1]['description'] == '-2 SYNCTIME'
```

### Step 8: Assign onset2 = value

```python
onset2 = raw.annotations[1]['onset']
```

### Step 9: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(out_file, apply_offsets=True)
```

**Verification:**
```python
assert raw.annotations[-1]['description'] == 'test string'
```

### Step 10: Call assert_allclose()

```python
assert_allclose(raw.annotations[-1]['onset'], onset1)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw.annotations[1]['onset'], onset2 - 2 / raw.info['sfreq'])
```

### Step 12: Assign lines = file.readlines(...)

```python
lines = file.readlines()
```

### Step 13: Call file.writelines()

```python
file.writelines(lines)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test read of annotations without offset.'
out_file = tmp_path / 'tmp_eyelink.asc'
with open(fname_href) as file:
    lines = file.readlines()
ts = lines[-3].split('\t')[0]
line = f'MSG\t{ts} test string\n'
lines = lines[:-3] + [line] + lines[-3:]
with open(out_file, 'w') as file:
    file.writelines(lines)
raw = read_raw_eyelink(out_file, apply_offsets=False)
assert raw.annotations[-1]['description'] == 'test string'
onset1 = raw.annotations[-1]['onset']
assert raw.annotations[1]['description'] == '-2 SYNCTIME'
onset2 = raw.annotations[1]['onset']
raw = read_raw_eyelink(out_file, apply_offsets=True)
assert raw.annotations[-1]['description'] == 'test string'
assert raw.annotations[1]['description'] == 'SYNCTIME'
assert_allclose(raw.annotations[-1]['onset'], onset1)
assert_allclose(raw.annotations[1]['onset'], onset2 - 2 / raw.info['sfreq'])
```

## Next Steps


---

*Source: test_eyelink.py:459 | Complexity: Advanced | Last updated: 2026-05-18*