# How To: Transforms

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test transformations.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `collections`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.bti.bti`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: pdf, config, hs, exported
```

## Step-by-Step Guide

### Step 1: 'Test transformations.'

```python
'Test transformations.'
```

**Verification:**
```python
assert_array_equal(dev_head_t_new['trans'], dev_head_t_old['trans'])
```

### Step 2: Assign bti_trans = value

```python
bti_trans = (0.0, 0.02, 0.11)
```

### Step 3: Assign bti_dev_t = Transform(...)

```python
bti_dev_t = Transform('ctf_meg', 'meg', _get_bti_dev_t(0.0, bti_trans))
```

### Step 4: Assign raw = read_raw_bti(...)

```python
raw = read_raw_bti(pdf, config, hs, preload=False)
```

### Step 5: Assign dev_ctf_t = value

```python
dev_ctf_t = raw.info['dev_ctf_t']
```

### Step 6: Assign dev_head_t_old = value

```python
dev_head_t_old = raw.info['dev_head_t']
```

### Step 7: Assign ctf_head_t = value

```python
ctf_head_t = raw.info['ctf_head_t']
```

### Step 8: Assign bti_dev_t = Transform(...)

```python
bti_dev_t = Transform('ctf_meg', 'meg', _get_bti_dev_t(0.0, bti_trans))
```

### Step 9: Assign t = combine_transforms(...)

```python
t = combine_transforms(invert_transform(bti_dev_t), dev_ctf_t, 'meg', 'ctf_head')
```

### Step 10: Assign dev_head_t_new = combine_transforms(...)

```python
dev_head_t_new = combine_transforms(t, ctf_head_t, 'meg', 'head')
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(dev_head_t_new['trans'], dev_head_t_old['trans'])
```


## Complete Example

```python
# Setup
# Fixtures: pdf, config, hs, exported

# Workflow
'Test transformations.'
bti_trans = (0.0, 0.02, 0.11)
bti_dev_t = Transform('ctf_meg', 'meg', _get_bti_dev_t(0.0, bti_trans))
raw = read_raw_bti(pdf, config, hs, preload=False)
dev_ctf_t = raw.info['dev_ctf_t']
dev_head_t_old = raw.info['dev_head_t']
ctf_head_t = raw.info['ctf_head_t']
bti_dev_t = Transform('ctf_meg', 'meg', _get_bti_dev_t(0.0, bti_trans))
t = combine_transforms(invert_transform(bti_dev_t), dev_ctf_t, 'meg', 'ctf_head')
dev_head_t_new = combine_transforms(t, ctf_head_t, 'meg', 'head')
assert_array_equal(dev_head_t_new['trans'], dev_head_t_old['trans'])
```

## Next Steps


---

*Source: test_bti.py:120 | Complexity: Advanced | Last updated: 2026-05-18*