# How To: Len Index Dipoles

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test len and indexing of Dipole objects.

## Prerequisites

**Required Modules:**
- `os`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.dipole`
- `mne.io`
- `mne.proj`
- `mne.simulation`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test len and indexing of Dipole objects.'

```python
'Test len and indexing of Dipole objects.'
```

### Step 2: Assign dipole = read_dipole(...)

```python
dipole = read_dipole(fname_dip)
```

### Step 3: Assign d0 = value

```python
d0 = dipole[0]
```

### Step 4: Assign d1 = value

```python
d1 = dipole[:1]
```

### Step 5: Call _check_dipole()

```python
_check_dipole(d0, 1)
```

### Step 6: Call _check_dipole()

```python
_check_dipole(d1, 1)
```

### Step 7: Call _compare_dipoles()

```python
_compare_dipoles(d0, d1)
```

### Step 8: Assign mask = value

```python
mask = dipole.gof > 15
```

### Step 9: Assign idx = value

```python
idx = np.where(mask)[0]
```

### Step 10: Assign d_mask = value

```python
d_mask = dipole[mask]
```

### Step 11: Call _check_dipole()

```python
_check_dipole(d_mask, 4)
```

### Step 12: Call _compare_dipoles()

```python
_compare_dipoles(d_mask, dipole[idx])
```


## Complete Example

```python
# Workflow
'Test len and indexing of Dipole objects.'
dipole = read_dipole(fname_dip)
d0 = dipole[0]
d1 = dipole[:1]
_check_dipole(d0, 1)
_check_dipole(d1, 1)
_compare_dipoles(d0, d1)
mask = dipole.gof > 15
idx = np.where(mask)[0]
d_mask = dipole[mask]
_check_dipole(d_mask, 4)
_compare_dipoles(d_mask, dipole[idx])
```

## Next Steps


---

*Source: test_dipole.py:315 | Complexity: Advanced | Last updated: 2026-05-18*