# How To: Acqparser Averaging

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test averaging with AcqParserFIF vs. Elekta software.

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test averaging with AcqParserFIF vs. Elekta software.'

```python
'Test averaging with AcqParserFIF vs. Elekta software.'
```

**Verification:**
```python
assert_allclose(ev_mag.data, ev_ref_mag.data, rtol=0, atol=1e-15)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw_elekta, preload=True)
```

**Verification:**
```python
assert ev_grad.ch_names == ev_ref_grad.ch_names
```

### Step 3: Assign acqp = AcqParserFIF(...)

```python
acqp = AcqParserFIF(raw.info)
```

**Verification:**
```python
assert_allclose(ev_grad.data, ev_ref_grad.data, rtol=0, atol=1e-13)
```

### Step 4: Assign cond = acqp.get_condition(...)

```python
cond = acqp.get_condition(raw, cat)
```

### Step 5: Assign eps = Epochs(...)

```python
eps = Epochs(raw, baseline=(-0.05, 0), **cond)
```

### Step 6: Assign ev = eps.average(...)

```python
ev = eps.average()
```

### Step 7: Assign ev_ref = read_evokeds(...)

```python
ev_ref = read_evokeds(fname_ave_elekta, cat['comment'], baseline=(-0.05, 0), proj=False)
```

### Step 8: Assign ev_mag = ev.copy(...)

```python
ev_mag = ev.copy()
```

### Step 9: Call ev_mag.pick()

```python
ev_mag.pick(['MEG0111'])
```

### Step 10: Assign ev_grad = ev.copy(...)

```python
ev_grad = ev.copy()
```

### Step 11: Call ev_grad.pick()

```python
ev_grad.pick(['MEG2643', 'MEG1622'])
```

### Step 12: Assign ev_ref_mag = ev_ref.copy(...)

```python
ev_ref_mag = ev_ref.copy()
```

### Step 13: Call ev_ref_mag.pick()

```python
ev_ref_mag.pick(['MEG0111'])
```

### Step 14: Assign ev_ref_grad = ev_ref.copy(...)

```python
ev_ref_grad = ev_ref.copy()
```

### Step 15: Call ev_ref_grad.pick()

```python
ev_ref_grad.pick(['MEG2643', 'MEG1622'])
```

### Step 16: Call assert_allclose()

```python
assert_allclose(ev_mag.data, ev_ref_mag.data, rtol=0, atol=1e-15)
```

**Verification:**
```python
assert ev_grad.ch_names == ev_ref_grad.ch_names
```

### Step 17: Call assert_allclose()

```python
assert_allclose(ev_grad.data, ev_ref_grad.data, rtol=0, atol=1e-13)
```


## Complete Example

```python
# Workflow
'Test averaging with AcqParserFIF vs. Elekta software.'
raw = read_raw_fif(fname_raw_elekta, preload=True)
acqp = AcqParserFIF(raw.info)
for cat in acqp.categories:
    cond = acqp.get_condition(raw, cat)
    eps = Epochs(raw, baseline=(-0.05, 0), **cond)
    ev = eps.average()
    ev_ref = read_evokeds(fname_ave_elekta, cat['comment'], baseline=(-0.05, 0), proj=False)
    ev_mag = ev.copy()
    ev_mag.pick(['MEG0111'])
    ev_grad = ev.copy()
    ev_grad.pick(['MEG2643', 'MEG1622'])
    ev_ref_mag = ev_ref.copy()
    ev_ref_mag.pick(['MEG0111'])
    ev_ref_grad = ev_ref.copy()
    ev_ref_grad.pick(['MEG2643', 'MEG1622'])
    assert_allclose(ev_mag.data, ev_ref_mag.data, rtol=0, atol=1e-15)
    assert ev_grad.ch_names == ev_ref_grad.ch_names
    assert_allclose(ev_grad.data, ev_ref_grad.data, rtol=0, atol=1e-13)
```

## Next Steps


---

*Source: test_event.py:573 | Complexity: Advanced | Last updated: 2026-05-18*