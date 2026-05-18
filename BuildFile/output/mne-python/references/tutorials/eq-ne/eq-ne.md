# How To: Eq Ne

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test == and != between projectors.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.proj`
- `mne.cov`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.proj`
- `mne.rank`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test == and != between projectors.'

```python
'Test == and != between projectors.'
```

**Verification:**
```python
assert len(raw.info['projs']) == 3
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=False)
```

**Verification:**
```python
assert pca1 != pca2
```

### Step 3: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

**Verification:**
```python
assert pca1 != car
```

### Step 4: Assign pca1 = cp.deepcopy(...)

```python
pca1 = cp.deepcopy(raw.info['projs'][0])
```

**Verification:**
```python
assert pca2 != car
```

### Step 5: Assign pca2 = cp.deepcopy(...)

```python
pca2 = cp.deepcopy(raw.info['projs'][1])
```

**Verification:**
```python
assert pca1 == raw.info['projs'][0]
```

### Step 6: Assign car = cp.deepcopy(...)

```python
car = cp.deepcopy(raw.info['projs'][3])
```

**Verification:**
```python
assert pca2 == raw.info['projs'][1]
```


## Complete Example

```python
# Workflow
'Test == and != between projectors.'
raw = read_raw_fif(raw_fname, preload=False)
assert len(raw.info['projs']) == 3
raw.set_eeg_reference(projection=True)
pca1 = cp.deepcopy(raw.info['projs'][0])
pca2 = cp.deepcopy(raw.info['projs'][1])
car = cp.deepcopy(raw.info['projs'][3])
assert pca1 != pca2
assert pca1 != car
assert pca2 != car
assert pca1 == raw.info['projs'][0]
assert pca2 == raw.info['projs'][1]
assert car == raw.info['projs'][3]
```

## Next Steps


---

*Source: test_proj.py:533 | Complexity: Intermediate | Last updated: 2026-05-18*