# How To: Vhdr Codepage Ansi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test BV reading with ANSI codepage.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test BV reading with ANSI codepage.'

```python
'Test BV reading with ANSI codepage.'
```

**Verification:**
```python
assert raw_init.ch_names == raw.ch_names
```

### Step 2: Assign raw_init = read_raw_brainvision(...)

```python
raw_init = read_raw_brainvision(vhdr_path)
```

**Verification:**
```python
assert_allclose(data_new, data_expected, atol=1e-15)
```

### Step 3: Assign unknown = value

```python
data_expected, times_expected = raw_init[:]
```

**Verification:**
```python
assert_allclose(times_new, times_expected, atol=1e-15)
```

### Step 4: Assign ansi_vhdr_path = value

```python
ansi_vhdr_path = tmp_path / vhdr_path.name
```

### Step 5: Assign ansi_vmrk_path = value

```python
ansi_vmrk_path = tmp_path / vmrk_path.name
```

### Step 6: Assign ansi_eeg_path = value

```python
ansi_eeg_path = tmp_path / eeg_path.name
```

### Step 7: Call shutil.copy()

```python
shutil.copy(eeg_path, ansi_eeg_path)
```

### Step 8: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(ansi_vhdr_path)
```

### Step 9: Assign unknown = value

```python
data_new, times_new = raw[:]
```

**Verification:**
```python
assert raw_init.ch_names == raw.ch_names
```

### Step 10: Call assert_allclose()

```python
assert_allclose(data_new, data_expected, atol=1e-15)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(times_new, times_expected, atol=1e-15)
```

### Step 12: Call fout.write()

```python
fout.write(line)
```

### Step 13: Call fout.write()

```python
fout.write(line)
```

### Step 14: Assign line = b'Codepage=ANSI\n'

```python
line = b'Codepage=ANSI\n'
```

### Step 15: Assign line = b'Codepage=ANSI\n'

```python
line = b'Codepage=ANSI\n'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test BV reading with ANSI codepage.'
raw_init = read_raw_brainvision(vhdr_path)
data_expected, times_expected = raw_init[:]
ansi_vhdr_path = tmp_path / vhdr_path.name
ansi_vmrk_path = tmp_path / vmrk_path.name
ansi_eeg_path = tmp_path / eeg_path.name
shutil.copy(eeg_path, ansi_eeg_path)
with open(ansi_vhdr_path, 'wb') as fout:
    with open(vhdr_path, 'rb') as fin:
        for line in fin:
            if line.startswith(b'Codepage'):
                line = b'Codepage=ANSI\n'
            fout.write(line)
with open(ansi_vmrk_path, 'wb') as fout:
    with open(vmrk_path, 'rb') as fin:
        for line in fin:
            if line.startswith(b'Codepage'):
                line = b'Codepage=ANSI\n'
            fout.write(line)
raw = read_raw_brainvision(ansi_vhdr_path)
data_new, times_new = raw[:]
assert raw_init.ch_names == raw.ch_names
assert_allclose(data_new, data_expected, atol=1e-15)
assert_allclose(times_new, times_expected, atol=1e-15)
```

## Next Steps


---

*Source: test_brainvision.py:176 | Complexity: Advanced | Last updated: 2026-05-18*