# How To: Drop Channels Mixin

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test channels-dropping functionality.

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

### Step 1: 'Test channels-dropping functionality.'

```python
'Test channels-dropping functionality.'
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

### Step 3: Assign drop_ch = value

```python
drop_ch = evoked.ch_names[:3]
```

**Verification:**
```python
assert_equal(len(ch_names_orig), len(evoked.data))
```

### Step 4: Assign ch_names = value

```python
ch_names = evoked.ch_names[3:]
```

**Verification:**
```python
assert_equal(dummy2.ch_names, ch_names_orig[1:])
```

### Step 5: Assign ch_names_orig = value

```python
ch_names_orig = evoked.ch_names
```

**Verification:**
```python
assert_equal(ch_names, evoked.ch_names)
```

### Step 6: Assign dummy = evoked.copy.drop_channels(...)

```python
dummy = evoked.copy().drop_channels(drop_ch)
```

**Verification:**
```python
assert_equal(len(ch_names), len(evoked.data))
```

### Step 7: Call assert_equal()

```python
assert_equal(ch_names, dummy.ch_names)
```

### Step 8: Call assert_equal()

```python
assert_equal(ch_names_orig, evoked.ch_names)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(ch_names_orig), len(evoked.data))
```

### Step 10: Assign dummy2 = evoked.copy.drop_channels(...)

```python
dummy2 = evoked.copy().drop_channels([drop_ch[0]])
```

### Step 11: Call assert_equal()

```python
assert_equal(dummy2.ch_names, ch_names_orig[1:])
```

### Step 12: Call evoked.drop_channels()

```python
evoked.drop_channels(drop_ch)
```

### Step 13: Call assert_equal()

```python
assert_equal(ch_names, evoked.ch_names)
```

### Step 14: Call assert_equal()

```python
assert_equal(len(ch_names), len(evoked.data))
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, evoked.drop_channels, ch_names)
```


## Complete Example

```python
# Workflow
'Test channels-dropping functionality.'
evoked = read_evokeds(fname, condition=0, proj=True)
drop_ch = evoked.ch_names[:3]
ch_names = evoked.ch_names[3:]
ch_names_orig = evoked.ch_names
dummy = evoked.copy().drop_channels(drop_ch)
assert_equal(ch_names, dummy.ch_names)
assert_equal(ch_names_orig, evoked.ch_names)
assert_equal(len(ch_names_orig), len(evoked.data))
dummy2 = evoked.copy().drop_channels([drop_ch[0]])
assert_equal(dummy2.ch_names, ch_names_orig[1:])
evoked.drop_channels(drop_ch)
assert_equal(ch_names, evoked.ch_names)
assert_equal(len(ch_names), len(evoked.data))
for ch_names in ([1, 2], 'fake', ['fake']):
    pytest.raises(ValueError, evoked.drop_channels, ch_names)
```

## Next Steps


---

*Source: test_evoked.py:629 | Complexity: Advanced | Last updated: 2026-05-18*