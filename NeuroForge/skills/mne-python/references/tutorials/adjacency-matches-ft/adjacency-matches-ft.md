# How To: Adjacency Matches Ft

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test correspondence of built-in adjacency matrices with FT repo.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, adj
```

## Step-by-Step Guide

### Step 1: 'Test correspondence of built-in adjacency matrices with FT repo.'

```python
'Test correspondence of built-in adjacency matrices with FT repo.'
```

**Verification:**
```python
assert hash_mne.hexdigest() == hash_ft.hexdigest(), f'Hash mismatch between built-in and FieldTrip neighbors for {fname}'
```

### Step 2: Assign builtin_neighbors_dir = value

```python
builtin_neighbors_dir = Path(__file__).parents[1] / 'data' / 'neighbors'
```

### Step 3: Assign ft_neighbors_dir = tmp_path

```python
ft_neighbors_dir = tmp_path
```

### Step 4: Assign fname = value

```python
fname = adj.fname
```

### Step 5: Call pooch.retrieve()

```python
pooch.retrieve(url=adj.source_url, known_hash=None, fname=fname, path=ft_neighbors_dir)
```

### Step 6: Assign hash_mne = hashlib.sha256(...)

```python
hash_mne = hashlib.sha256()
```

### Step 7: Assign hash_ft = hashlib.sha256(...)

```python
hash_ft = hashlib.sha256()
```

### Step 8: Call hash_mne.update()

```python
hash_mne.update((builtin_neighbors_dir / fname).read_bytes())
```

### Step 9: Call hash_ft.update()

```python
hash_ft.update((ft_neighbors_dir / fname).read_bytes())
```

**Verification:**
```python
assert hash_mne.hexdigest() == hash_ft.hexdigest(), f'Hash mismatch between built-in and FieldTrip neighbors for {fname}'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, adj

# Workflow
'Test correspondence of built-in adjacency matrices with FT repo.'
builtin_neighbors_dir = Path(__file__).parents[1] / 'data' / 'neighbors'
ft_neighbors_dir = tmp_path
del tmp_path
fname = adj.fname
pooch.retrieve(url=adj.source_url, known_hash=None, fname=fname, path=ft_neighbors_dir)
hash_mne = hashlib.sha256()
hash_ft = hashlib.sha256()
hash_mne.update((builtin_neighbors_dir / fname).read_bytes())
hash_ft.update((ft_neighbors_dir / fname).read_bytes())
assert hash_mne.hexdigest() == hash_ft.hexdigest(), f'Hash mismatch between built-in and FieldTrip neighbors for {fname}'
```

## Next Steps


---

*Source: test_channels.py:365 | Complexity: Advanced | Last updated: 2026-05-18*