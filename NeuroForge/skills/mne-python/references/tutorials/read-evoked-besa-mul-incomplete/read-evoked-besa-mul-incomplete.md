# How To: Read Evoked Besa Mul Incomplete

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading incomplete BESA .mul files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `inspect`
- `pathlib`
- `pytest`
- `mne.channels`
- `mne.io`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading incomplete BESA .mul files.'

```python
'Test reading incomplete BESA .mul files.'
```

**Verification:**
```python
assert len(ev.ch_names) == len(ev.data) == 1
```

### Step 2: Assign ev = read_evoked_besa(...)

```python
ev = read_evoked_besa(f'{tmp_path}/missing.mul')
```

**Verification:**
```python
assert ev.info['sfreq'] == 200
```

### Step 3: Call f.write()

```python
f.write('SamplingInterval[ms]= 5\nCH1\n0\n')
```

**Verification:**
```python
assert ev.tmin == 0
```

### Step 4: Call f.write()

```python
f.write('TimePoints= 1 Channels= 1\nCH1\n0\n')
```

**Verification:**
```python
assert len(ev.times) == 1
```

### Step 5: Assign ev = read_evoked_besa(...)

```python
ev = read_evoked_besa(f'{tmp_path}/missing.mul')
```

**Verification:**
```python
assert ev.ch_names == ['CH1']
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading incomplete BESA .mul files.'
with open(f'{tmp_path}/missing.mul', 'w') as f:
    f.write('SamplingInterval[ms]= 5\nCH1\n0\n')
ev = read_evoked_besa(f'{tmp_path}/missing.mul')
assert len(ev.ch_names) == len(ev.data) == 1
assert ev.info['sfreq'] == 200
assert ev.tmin == 0
assert len(ev.times) == 1
assert ev.ch_names == ['CH1']
assert ev.comment == ''
with open(f'{tmp_path}/missing.mul', 'w') as f:
    f.write('TimePoints= 1 Channels= 1\nCH1\n0\n')
with pytest.raises(RuntimeError, match='No "SamplingInterval\\[ms\\]"'):
    ev = read_evoked_besa(f'{tmp_path}/missing.mul')
```

## Next Steps


---

*Source: test_besa.py:62 | Complexity: Intermediate | Last updated: 2026-05-18*