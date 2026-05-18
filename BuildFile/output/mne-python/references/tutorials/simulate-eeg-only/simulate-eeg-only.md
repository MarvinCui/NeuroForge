# How To: Simulate Eeg Only

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test simulate_raw with EEG data only.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.chpi`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.simulation`
- `mne.simulation.source`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.tests.test_chpi`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: raw_data
```

## Step-by-Step Guide

### Step 1: 'Test simulate_raw with EEG data only.'

```python
'Test simulate_raw with EEG data only.'
```

**Verification:**
```python
assert raw.info['dev_head_t'] is not None
```

### Step 2: Assign unknown = raw_data

```python
raw, src, stc, trans, sphere = raw_data
```

**Verification:**
```python
assert fwd['info']['dev_head_t'] is None
```

### Step 3: Assign raw = raw.pick(...)

```python
raw = raw.pick('eeg')
```

**Verification:**
```python
assert raw_sim.info['dev_head_t'] is None
```

### Step 4: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(raw.info, trans, src, sphere)
```

**Verification:**
```python
assert raw_sim_2.info['dev_head_t'] is None
```

### Step 5: Assign raw_sim = simulate_raw(...)

```python
raw_sim = simulate_raw(raw.info, stc, None, None, None, forward=fwd)
```

**Verification:**
```python
assert_allclose(raw_sim[:][0], raw_sim_2[:][0])
```

### Step 6: Assign unknown = Transform(...)

```python
fwd['info']['dev_head_t'] = Transform('meg', 'head')
```

### Step 7: Assign raw_sim_2 = simulate_raw(...)

```python
raw_sim_2 = simulate_raw(raw.info, stc, None, None, None, forward=fwd)
```

**Verification:**
```python
assert raw_sim.info['dev_head_t'] is None
```

### Step 8: Call assert_allclose()

```python
assert_allclose(raw_sim[:][0], raw_sim_2[:][0])
```

### Step 9: Assign unknown = None

```python
raw.info['dev_head_t'] = None
```


## Complete Example

```python
# Setup
# Fixtures: raw_data

# Workflow
'Test simulate_raw with EEG data only.'
raw, src, stc, trans, sphere = raw_data
raw = raw.pick('eeg')
assert raw.info['dev_head_t'] is not None
with raw.info._unlock():
    raw.info['dev_head_t'] = None
fwd = make_forward_solution(raw.info, trans, src, sphere)
assert fwd['info']['dev_head_t'] is None
raw_sim = simulate_raw(raw.info, stc, None, None, None, forward=fwd)
fwd['info']['dev_head_t'] = Transform('meg', 'head')
raw_sim_2 = simulate_raw(raw.info, stc, None, None, None, forward=fwd)
assert raw_sim.info['dev_head_t'] is None
assert raw_sim_2.info['dev_head_t'] is None
assert_allclose(raw_sim[:][0], raw_sim_2[:][0])
```

## Next Steps


---

*Source: test_raw.py:504 | Complexity: Advanced | Last updated: 2026-05-18*