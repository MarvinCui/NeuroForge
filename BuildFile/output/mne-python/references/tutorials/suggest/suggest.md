# How To: Suggest

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test suggestions.

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.utils`
- `types`


## Step-by-Step Guide

### Step 1: 'Test suggestions.'

```python
'Test suggestions.'
```

**Verification:**
```python
assert sug == ''
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert sug == " Did you mean 'Left-Cerebellum-Cortex'?"
```

### Step 3: Assign names = mne.get_volume_labels_from_aseg(...)

```python
names = mne.get_volume_labels_from_aseg(fname_mgz)
```

**Verification:**
```python
assert sug == " Did you mean one of ['Left-Cerebellum-Cortex', 'Right-Cerebellum-Cortex', 'Left-Cerebral-Cortex']?"
```

### Step 4: Assign sug = _suggest(...)

```python
sug = _suggest('', names)
```

**Verification:**
```python
assert sug == ''
```

### Step 5: Assign sug = _suggest(...)

```python
sug = _suggest('Left-cerebellum', names)
```

**Verification:**
```python
assert sug == " Did you mean 'Left-Cerebellum-Cortex'?"
```

### Step 6: Assign sug = _suggest(...)

```python
sug = _suggest('Cerebellum-Cortex', names)
```

**Verification:**
```python
assert sug == " Did you mean one of ['Left-Cerebellum-Cortex', 'Right-Cerebellum-Cortex', 'Left-Cerebral-Cortex']?"
```


## Complete Example

```python
# Workflow
'Test suggestions.'
pytest.importorskip('nibabel')
names = mne.get_volume_labels_from_aseg(fname_mgz)
sug = _suggest('', names)
assert sug == ''
sug = _suggest('Left-cerebellum', names)
assert sug == " Did you mean 'Left-Cerebellum-Cortex'?"
sug = _suggest('Cerebellum-Cortex', names)
assert sug == " Did you mean one of ['Left-Cerebellum-Cortex', 'Right-Cerebellum-Cortex', 'Left-Cerebral-Cortex']?"
```

## Next Steps


---

*Source: test_check.py:261 | Complexity: Intermediate | Last updated: 2026-05-18*