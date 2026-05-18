# How To: Find Eog

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test find EOG peaks.

## Prerequisites

**Required Modules:**
- `pathlib`
- `mne`
- `mne.io`
- `mne.preprocessing.eog`


## Step-by-Step Guide

### Step 1: 'Test find EOG peaks.'

```python
'Test find EOG peaks.'
```

**Verification:**
```python
assert len(events) == 4
```

### Step 2: Assign ch_name = 'EOG 061'

```python
ch_name = 'EOG 061'
```

**Verification:**
```python
assert not all(events[:, 0] < 29000)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert all(events[:, 0] < 29000)
```

### Step 4: Call raw.set_annotations()

```python
raw.set_annotations(Annotations([14, 21], [1, 1], 'BAD_blink'))
```

**Verification:**
```python
assert len(events_thr) == 5
```

### Step 5: Assign events = find_eog_events(...)

```python
events = find_eog_events(raw, ch_name=ch_name)
```

**Verification:**
```python
assert len(events) == 4
```

### Step 6: Assign events = find_eog_events(...)

```python
events = find_eog_events(raw, reject_by_annotation=True, ch_name=ch_name)
```

**Verification:**
```python
assert len(events) == 4
```

### Step 7: Assign events_thr = find_eog_events(...)

```python
events_thr = find_eog_events(raw, thresh=0.0001, ch_name=ch_name)
```

**Verification:**
```python
assert len(events_thr) == 5
```

### Step 8: Assign events = find_eog_events(...)

```python
events = find_eog_events(raw, ch_name=None)
```

**Verification:**
```python
assert len(events) == 4
```

### Step 9: Assign events = find_eog_events(...)

```python
events = find_eog_events(raw, ch_name=['EEG 060', 'EOG 061'])
```

**Verification:**
```python
assert len(events) == 4
```


## Complete Example

```python
# Workflow
'Test find EOG peaks.'
ch_name = 'EOG 061'
raw = read_raw_fif(raw_fname)
raw.set_annotations(Annotations([14, 21], [1, 1], 'BAD_blink'))
events = find_eog_events(raw, ch_name=ch_name)
assert len(events) == 4
assert not all(events[:, 0] < 29000)
events = find_eog_events(raw, reject_by_annotation=True, ch_name=ch_name)
assert all(events[:, 0] < 29000)
events_thr = find_eog_events(raw, thresh=0.0001, ch_name=ch_name)
assert len(events_thr) == 5
events = find_eog_events(raw, ch_name=None)
assert len(events) == 4
events = find_eog_events(raw, ch_name=['EEG 060', 'EOG 061'])
assert len(events) == 4
```

## Next Steps


---

*Source: test_eog.py:17 | Complexity: Advanced | Last updated: 2026-05-18*