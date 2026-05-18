# How To: Pick Channels Mixin

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test channel-picking functionality.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test channel-picking functionality.'

```python
'Test channel-picking functionality.'
```

**Verification:**
```python
assert_equal(ch_names, dummy.ch_names)
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname, condition=0, proj=True)
```

**Verification:**
```python
assert_equal(ch_names_orig, evoked.ch_names)
```

### Step 3: Assign ch_names = value

```python
ch_names = evoked.ch_names[:3]
```

**Verification:**
```python
assert_equal(len(ch_names_orig), len(evoked.data))
```

### Step 4: Assign ch_names_orig = value

```python
ch_names_orig = evoked.ch_names
```

**Verification:**
```python
assert_equal(ch_names, evoked.ch_names)
```

### Step 5: Assign dummy = evoked.copy.pick(...)

```python
dummy = evoked.copy().pick(ch_names)
```

**Verification:**
```python
assert_equal(len(ch_names), len(evoked.data))
```

### Step 6: Call assert_equal()

```python
assert_equal(ch_names, dummy.ch_names)
```

**Verification:**
```python
assert 'meg' in evoked
```

### Step 7: Call assert_equal()

```python
assert_equal(ch_names_orig, evoked.ch_names)
```

**Verification:**
```python
assert 'eeg' in evoked
```

### Step 8: Call assert_equal()

```python
assert_equal(len(ch_names_orig), len(evoked.data))
```

**Verification:**
```python
assert 'meg' not in evoked
```

### Step 9: Call evoked.pick()

```python
evoked.pick(ch_names)
```

**Verification:**
```python
assert 'eeg' in evoked
```

### Step 10: Call assert_equal()

```python
assert_equal(ch_names, evoked.ch_names)
```

**Verification:**
```python
assert len(evoked.ch_names) == 60
```

### Step 11: Call assert_equal()

```python
assert_equal(len(ch_names), len(evoked.data))
```

### Step 12: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(fname, condition=0, proj=True)
```

**Verification:**
```python
assert 'meg' in evoked
```

### Step 13: Call evoked.pick()

```python
evoked.pick(picks='eeg')
```

**Verification:**
```python
assert 'meg' not in evoked
```


## Complete Example

```python
# Workflow
'Test channel-picking functionality.'
evoked = read_evokeds(fname, condition=0, proj=True)
ch_names = evoked.ch_names[:3]
ch_names_orig = evoked.ch_names
dummy = evoked.copy().pick(ch_names)
assert_equal(ch_names, dummy.ch_names)
assert_equal(ch_names_orig, evoked.ch_names)
assert_equal(len(ch_names_orig), len(evoked.data))
evoked.pick(ch_names)
assert_equal(ch_names, evoked.ch_names)
assert_equal(len(ch_names), len(evoked.data))
evoked = read_evokeds(fname, condition=0, proj=True)
assert 'meg' in evoked
assert 'eeg' in evoked
evoked.pick(picks='eeg')
assert 'meg' not in evoked
assert 'eeg' in evoked
assert len(evoked.ch_names) == 60
```

## Next Steps


---

*Source: test_evoked.py:651 | Complexity: Advanced | Last updated: 2026-05-18*