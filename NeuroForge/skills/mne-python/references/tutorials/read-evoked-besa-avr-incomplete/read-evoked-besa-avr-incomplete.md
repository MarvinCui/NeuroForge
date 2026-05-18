# How To: Read Evoked Besa Avr Incomplete

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading incomplete BESA .avr files.

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

### Step 1: 'Test reading incomplete BESA .avr files.'

```python
'Test reading incomplete BESA .avr files.'
```

**Verification:**
```python
assert ev.ch_names == ['CH01', 'CH02', 'CH03']
```

### Step 2: Assign ev = read_evoked_besa(...)

```python
ev = read_evoked_besa(f'{tmp_path}/missing.avr')
```

**Verification:**
```python
assert len(ev.ch_names) == len(ev.data) == 1
```

### Step 3: Assign ev = read_evoked_besa(...)

```python
ev = read_evoked_besa(f'{tmp_path}/missing.avr')
```

**Verification:**
```python
assert ev.info['sfreq'] == 200
```

### Step 4: Call f.write()

```python
f.write('Npts= 1  TSB= 0  SB= 1.00  SC= 500.0  DI= 5\n0\n1\n2\n')
```

**Verification:**
```python
assert ev.tmin == 0
```

### Step 5: Call f.write()

```python
f.write('DI= 5\n0\n')
```

**Verification:**
```python
assert len(ev.times) == 1
```

### Step 6: Call f.write()

```python
f.write('Npts= 1  TSB= 0  SB= 1.00  SC= 500.0\n0\n')
```

**Verification:**
```python
assert ev.ch_names == ['CH01']
```

### Step 7: Assign ev = read_evoked_besa(...)

```python
ev = read_evoked_besa(f'{tmp_path}/missing.avr')
```

**Verification:**
```python
assert ev.comment == ''
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading incomplete BESA .avr files.'
with open(f'{tmp_path}/missing.avr', 'w') as f:
    f.write('Npts= 1  TSB= 0  SB= 1.00  SC= 500.0  DI= 5\n0\n1\n2\n')
ev = read_evoked_besa(f'{tmp_path}/missing.avr')
assert ev.ch_names == ['CH01', 'CH02', 'CH03']
with open(f'{tmp_path}/missing.avr', 'w') as f:
    f.write('DI= 5\n0\n')
ev = read_evoked_besa(f'{tmp_path}/missing.avr')
assert len(ev.ch_names) == len(ev.data) == 1
assert ev.info['sfreq'] == 200
assert ev.tmin == 0
assert len(ev.times) == 1
assert ev.ch_names == ['CH01']
assert ev.comment == ''
with open(f'{tmp_path}/missing.avr', 'w') as f:
    f.write('Npts= 1  TSB= 0  SB= 1.00  SC= 500.0\n0\n')
with pytest.raises(RuntimeError, match='No "DI" field present'):
    ev = read_evoked_besa(f'{tmp_path}/missing.avr')
```

## Next Steps


---

*Source: test_besa.py:36 | Complexity: Intermediate | Last updated: 2026-05-18*