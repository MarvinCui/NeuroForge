# How To: Io Amp Disconnection

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test loading of .cnt file with amplifier disconnection.

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

### Step 1: 'Test loading of .cnt file with amplifier disconnection.'

```python
'Test loading of .cnt file with amplifier disconnection.'
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

### Step 2: Assign raw_cnt = read_raw_ant(...)

```python
raw_cnt = read_raw_ant(ca_208['cnt']['amp-dc'])
```

**Verification:**
```python
assert raw_cnt.get_data(reject_by_annotation='omit').shape != raw_bv.get_data().shape
```

### Step 3: Assign raw_bv = read_raw_bv(...)

```python
raw_bv = read_raw_bv(ca_208['bv']['amp-dc'])
```

**Verification:**
```python
assert len(idx) == 2
```

### Step 4: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
```

**Verification:**
```python
assert_allclose(raw_cnt.get_data(reject_by_annotation='omit'), raw_bv.get_data(reject_by_annotation='omit'), atol=1e-08)
```

### Step 5: Assign idx = value

```python
idx = [k for k, elt in enumerate(raw_bv.annotations.description) if any((code in elt for code in ('9001', '9002')))]
```

**Verification:**
```python
assert len(idx) == 2
```

### Step 6: Assign start = value

```python
start = raw_bv.annotations.onset[idx[0]]
```

### Step 7: Assign stop = value

```python
stop = raw_bv.annotations.onset[idx[1]]
```

### Step 8: Assign annotations = Annotations(...)

```python
annotations = Annotations(onset=start, duration=stop - start + 1 / raw_bv.info['sfreq'], description='BAD_segment')
```

### Step 9: Call raw_bv.set_annotations()

```python
raw_bv.set_annotations(annotations)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(raw_cnt.get_data(reject_by_annotation='omit'), raw_bv.get_data(reject_by_annotation='omit'), atol=1e-08)
```


## Complete Example

```python
# Setup
# Fixtures: ca_208

# Workflow
'Test loading of .cnt file with amplifier disconnection.'
raw_cnt = read_raw_ant(ca_208['cnt']['amp-dc'])
raw_bv = read_raw_bv(ca_208['bv']['amp-dc'])
assert_allclose(raw_cnt.get_data(), raw_bv.get_data(), atol=1e-08)
assert raw_cnt.get_data(reject_by_annotation='omit').shape != raw_bv.get_data().shape
idx = [k for k, elt in enumerate(raw_bv.annotations.description) if any((code in elt for code in ('9001', '9002')))]
assert len(idx) == 2
start = raw_bv.annotations.onset[idx[0]]
stop = raw_bv.annotations.onset[idx[1]]
annotations = Annotations(onset=start, duration=stop - start + 1 / raw_bv.info['sfreq'], description='BAD_segment')
raw_bv.set_annotations(annotations)
assert_allclose(raw_cnt.get_data(reject_by_annotation='omit'), raw_bv.get_data(reject_by_annotation='omit'), atol=1e-08)
```

## Next Steps


---

*Source: test_ant.py:359 | Complexity: Advanced | Last updated: 2026-05-18*