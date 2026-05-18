# How To: Plot Defect Montage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting defect montages (i.e. with duplicate labels).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.io`

**Setup Required:**
```python
# Fixtures: name, n
```

## Step-by-Step Guide

### Step 1: 'Test plotting defect montages (i.e. with duplicate labels).'

```python
'Test plotting defect montages (i.e. with duplicate labels).'
```

**Verification:**
```python
assert collection._edgecolors.shape[0] == n
```

### Step 2: Assign m = make_standard_montage(...)

```python
m = make_standard_montage(name)
```

**Verification:**
```python
assert collection._facecolors.shape[0] == n
```

### Step 3: Assign fig = m.plot(...)

```python
fig = m.plot()
```

**Verification:**
```python
assert collection._offsets.shape[0] == n
```

### Step 4: Assign collection = value

```python
collection = fig.axes[0].collections[0]
```

**Verification:**
```python
assert collection._edgecolors.shape[0] == n
```


## Complete Example

```python
# Setup
# Fixtures: name, n

# Workflow
'Test plotting defect montages (i.e. with duplicate labels).'
m = make_standard_montage(name)
n -= 3
fig = m.plot()
collection = fig.axes[0].collections[0]
assert collection._edgecolors.shape[0] == n
assert collection._facecolors.shape[0] == n
assert collection._offsets.shape[0] == n
```

## Next Steps


---

*Source: test_montage.py:72 | Complexity: Intermediate | Last updated: 2026-05-18*