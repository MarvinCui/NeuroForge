# How To: Io Info Parse Eog

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parsing EOG channels from a .cnt file.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.ant.ant`

**Setup Required:**
```python
# Fixtures: ca_208
```

## Step-by-Step Guide

### Step 1: 'Test parsing EOG channels from a .cnt file.'

```python
'Test parsing EOG channels from a .cnt file.'
```

**Verification:**
```python
assert len(raw_cnt.ch_names) == ca_208['n_eeg'] + ca_208['n_misc']
```

### Step 2: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(ca_208['cnt']['short'], eog='EOG')
```

**Verification:**
```python
assert raw_cnt.get_channel_types() == ch_types
```

### Step 3: Assign idx = raw_cnt.ch_names.index(...)

```python
idx = raw_cnt.ch_names.index('EOG')
```

### Step 4: Assign ch_types = value

```python
ch_types = ['eeg'] * ca_208['n_eeg'] + ['misc'] * ca_208['n_misc']
```

### Step 5: Assign unknown = 'eog'

```python
ch_types[idx] = 'eog'
```

**Verification:**
```python
assert raw_cnt.get_channel_types() == ch_types
```


## Complete Example

```python
# Setup
# Fixtures: ca_208

# Workflow
'Test parsing EOG channels from a .cnt file.'
raw_cnt = read_raw_ant(ca_208['cnt']['short'], eog='EOG')
assert len(raw_cnt.ch_names) == ca_208['n_eeg'] + ca_208['n_misc']
idx = raw_cnt.ch_names.index('EOG')
ch_types = ['eeg'] * ca_208['n_eeg'] + ['misc'] * ca_208['n_misc']
ch_types[idx] = 'eog'
assert raw_cnt.get_channel_types() == ch_types
```

## Next Steps


---

*Source: test_ant.py:315 | Complexity: Intermediate | Last updated: 2026-05-18*