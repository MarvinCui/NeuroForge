# How To: Plot Epochs Scale Bar

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test scale bar for epochs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.utils`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: epochs, browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test scale bar for epochs.'

```python
'Test scale bar for epochs.'
```

**Verification:**
```python
assert len(texts) == 2
```

### Step 2: Assign fig = epochs.plot(...)

```python
fig = epochs.plot()
```

**Verification:**
```python
assert len(texts) == 4
```

### Step 3: Assign texts = fig._get_scale_bar_texts(...)

```python
texts = fig._get_scale_bar_texts()
```

**Verification:**
```python
assert texts == wants
```

### Step 4: Assign wants = value

```python
wants = ('800.0 fT/cm', '2000.0 fT')
```

**Verification:**
```python
assert len(texts) == 4
```

### Step 5: Assign wants = value

```python
wants = ('800.0 fT/cm', '0.55 s', '2000.0 fT', '0.55 s')
```


## Complete Example

```python
# Setup
# Fixtures: epochs, browser_backend

# Workflow
'Test scale bar for epochs.'
fig = epochs.plot()
texts = fig._get_scale_bar_texts()
if browser_backend.name == 'pyqtgraph':
    assert len(texts) == 2
    wants = ('800.0 fT/cm', '2000.0 fT')
elif browser_backend.name == 'matplotlib':
    assert len(texts) == 4
    wants = ('800.0 fT/cm', '0.55 s', '2000.0 fT', '0.55 s')
assert texts == wants
```

## Next Steps


---

*Source: test_epochs.py:97 | Complexity: Intermediate | Last updated: 2026-05-18*