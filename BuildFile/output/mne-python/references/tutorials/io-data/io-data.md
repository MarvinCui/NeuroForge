# How To: Io Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test loading of .cnt file.

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
# Fixtures: dataset, request
```

## Step-by-Step Guide

### Step 1: 'Test loading of .cnt file.'

```python
'Test loading of .cnt file.'
```

**Verification:**
```python
assert cnt.shape == bv.shape
```

### Step 2: Assign dataset = request.getfixturevalue(...)

```python
dataset = request.getfixturevalue(dataset)
```

**Verification:**
```python
assert_allclose(cnt, bv, atol=1e-08)
```

### Step 3: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(dataset['cnt']['short'])
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_cnt2.get_data())
```

### Step 4: Assign raw_bv = read_raw_bv(...)

```python
raw_bv = read_raw_bv(dataset['bv']['short'])
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 5: Assign cnt = raw_cnt.get_data(...)

```python
cnt = raw_cnt.get_data()
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 6: Assign bv = raw_bv.get_data(...)

```python
bv = raw_bv.get_data()
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(cnt, bv, atol=1e-08)
```

**Verification:**
```python
assert_allclose(raw_cnt.drop_channels(bads).get_data(), raw_cnt2.drop_channels(bads).get_data())
```

### Step 8: Call raw_cnt.crop()

```python
raw_cnt.crop(0.05, 1.05)
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 9: Assign raw_cnt2 = read_raw_ant(...)

```python
raw_cnt2 = read_raw_ant(dataset['cnt']['short'], preload=False)
```

**Verification:**
```python
assert_allclose(raw_cnt2.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 10: Call raw_cnt2.crop.load_data()

```python
raw_cnt2.crop(0.05, 1.05).load_data()
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_cnt2.get_data())
```

### Step 12: Call raw_bv.crop()

```python
raw_bv.crop(0.05, 1.05)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 14: Call raw_cnt.pick()

```python
raw_cnt.pick(raw_cnt.ch_names[::2])
```

### Step 15: Call raw_bv.pick()

```python
raw_bv.pick(raw_bv.ch_names[::2])
```

### Step 16: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 17: Call raw_cnt.load_data()

```python
raw_cnt.load_data()
```

### Step 18: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 19: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(dataset['cnt']['short'], preload=False)
```

### Step 20: Assign raw_cnt2 = read_raw_ant(...)

```python
raw_cnt2 = read_raw_ant(dataset['cnt']['short'], preload=True)
```

### Step 21: Assign bads = value

```python
bads = [raw_cnt.ch_names[idx] for idx in (1, 5, 10)]
```

### Step 22: Call assert_allclose()

```python
assert_allclose(raw_cnt.drop_channels(bads).get_data(), raw_cnt2.drop_channels(bads).get_data())
```

### Step 23: Assign raw_bv = read_raw_bv.drop_channels(...)

```python
raw_bv = read_raw_bv(dataset['bv']['short']).drop_channels(bads)
```

### Step 24: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 25: Call assert_allclose()

```python
assert_allclose(raw_cnt2.get_data(), raw_bv.get_data(), atol=1e-08)
```


## Complete Example

```python
# Setup
# Fixtures: dataset, request

# Workflow
'Test loading of .cnt file.'
dataset = request.getfixturevalue(dataset)
raw_cnt = read_raw_ant(dataset['cnt']['short'])
raw_bv = read_raw_bv(dataset['bv']['short'])
cnt = raw_cnt.get_data()
bv = raw_bv.get_data()
assert cnt.shape == bv.shape
assert_allclose(cnt, bv, atol=1e-08)
raw_cnt.crop(0.05, 1.05)
raw_cnt2 = read_raw_ant(dataset['cnt']['short'], preload=False)
raw_cnt2.crop(0.05, 1.05).load_data()
assert_allclose(raw_cnt.get_data(), raw_cnt2.get_data())
raw_bv.crop(0.05, 1.05)
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
raw_cnt.pick(raw_cnt.ch_names[::2])
raw_bv.pick(raw_bv.ch_names[::2])
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
raw_cnt.load_data()
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
raw_cnt = read_raw_ant(dataset['cnt']['short'], preload=False)
raw_cnt2 = read_raw_ant(dataset['cnt']['short'], preload=True)
bads = [raw_cnt.ch_names[idx] for idx in (1, 5, 10)]
assert_allclose(raw_cnt.drop_channels(bads).get_data(), raw_cnt2.drop_channels(bads).get_data())
raw_bv = read_raw_bv(dataset['bv']['short']).drop_channels(bads)
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
assert_allclose(raw_cnt2.get_data(), raw_bv.get_data(), atol=1e-08)
```

## Next Steps


---

*Source: test_ant.py:221 | Complexity: Advanced | Last updated: 2026-05-18*