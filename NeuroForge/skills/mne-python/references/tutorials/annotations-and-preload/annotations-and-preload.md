# How To: Annotations And Preload

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test annotation loading with preload True/False.

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

### Step 1: 'Test annotation loading with preload True/False.'

```python
'Test annotation loading with preload True/False.'
```

**Verification:**
```python
assert len(raw_cnt_preloaded.annotations) == 2
```

### Step 2: Assign raw_cnt_preloaded = read_raw_ant(...)

```python
raw_cnt_preloaded = read_raw_ant(ca_208['cnt']['short'], preload=True)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 2
```

### Step 3: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(ca_208['cnt']['short'], preload=False)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 0
```

### Step 4: Call raw_cnt.crop()

```python
raw_cnt.crop(2, 3)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 0
```

### Step 5: Call raw_cnt.load_data()

```python
raw_cnt.load_data()
```

**Verification:**
```python
assert len(raw_cnt_preloaded.annotations) == 5
```

### Step 6: Assign raw_cnt_preloaded = read_raw_ant(...)

```python
raw_cnt_preloaded = read_raw_ant(ca_208['cnt']['amp-dc'], preload=True)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 5
```

### Step 7: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(ca_208['cnt']['amp-dc'], preload=False)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 1
```

### Step 8: Assign idx = value

```python
idx = np.where(raw_cnt.annotations.description == 'BAD_disconnection')[0]
```

**Verification:**
```python
assert raw_cnt.annotations.description[0] == 'impedance'
```

### Step 9: Assign onset = value

```python
onset = raw_cnt.annotations.onset[idx][0]
```

### Step 10: Call raw_cnt.crop()

```python
raw_cnt.crop(0, onset - 1)
```

**Verification:**
```python
assert len(raw_cnt.annotations) == 1
```


## Complete Example

```python
# Setup
# Fixtures: ca_208

# Workflow
'Test annotation loading with preload True/False.'
raw_cnt_preloaded = read_raw_ant(ca_208['cnt']['short'], preload=True)
assert len(raw_cnt_preloaded.annotations) == 2
raw_cnt = read_raw_ant(ca_208['cnt']['short'], preload=False)
assert len(raw_cnt.annotations) == 2
raw_cnt.crop(2, 3)
assert len(raw_cnt.annotations) == 0
raw_cnt.load_data()
assert len(raw_cnt.annotations) == 0
raw_cnt_preloaded = read_raw_ant(ca_208['cnt']['amp-dc'], preload=True)
assert len(raw_cnt_preloaded.annotations) == 5
raw_cnt = read_raw_ant(ca_208['cnt']['amp-dc'], preload=False)
assert len(raw_cnt.annotations) == 5
idx = np.where(raw_cnt.annotations.description == 'BAD_disconnection')[0]
onset = raw_cnt.annotations.onset[idx][0]
raw_cnt.crop(0, onset - 1)
assert len(raw_cnt.annotations) == 1
assert raw_cnt.annotations.description[0] == 'impedance'
```

## Next Steps


---

*Source: test_ant.py:409 | Complexity: Advanced | Last updated: 2026-05-18*