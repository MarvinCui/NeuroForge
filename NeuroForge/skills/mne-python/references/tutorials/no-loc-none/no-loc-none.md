# How To: No Loc None

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test that we don't set loc to None when no trans is found.

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
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: "Test that we don't set loc to None when no trans is found."

```python
"Test that we don't set loc to None when no trans is found."
```

**Verification:**
```python
assert_allclose(raw.info['chs'][idx]['loc'], np.full(12, np.nan))
```

### Step 2: Assign ch_name = 'MLzA'

```python
ch_name = 'MLzA'
```

### Step 3: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.io.bti.bti, '_read_config', _read_config_bad)
```

### Step 4: Assign kwargs = dict(...)

```python
kwargs = dict(pdf_fname=pdf_fnames[0], config_fname=config_fnames[0], head_shape_fname=hs_fnames[0], rename_channels=False, sort_by_ch_name=False)
```

### Step 5: Assign raw = read_raw_bti(...)

```python
raw = read_raw_bti(**kwargs)
```

### Step 6: Assign idx = raw.ch_names.index(...)

```python
idx = raw.ch_names.index(ch_name)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw.info['chs'][idx]['loc'], np.full(12, np.nan))
```

### Step 8: Assign cfg = _read_config(...)

```python
cfg = _read_config(*args, **kwargs)
```

### Step 9: Assign idx = unknown.index(...)

```python
idx = [ch['name'] for ch in cfg['chs']].index(ch_name)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
"Test that we don't set loc to None when no trans is found."
ch_name = 'MLzA'

def _read_config_bad(*args, **kwargs):
    cfg = _read_config(*args, **kwargs)
    idx = [ch['name'] for ch in cfg['chs']].index(ch_name)
    del cfg['chs'][idx]['dev']['transform']
    return cfg
monkeypatch.setattr(mne.io.bti.bti, '_read_config', _read_config_bad)
kwargs = dict(pdf_fname=pdf_fnames[0], config_fname=config_fnames[0], head_shape_fname=hs_fnames[0], rename_channels=False, sort_by_ch_name=False)
raw = read_raw_bti(**kwargs)
idx = raw.ch_names.index(ch_name)
assert_allclose(raw.info['chs'][idx]['loc'], np.full(12, np.nan))
```

## Next Steps


---

*Source: test_bti.py:68 | Complexity: Advanced | Last updated: 2026-05-18*