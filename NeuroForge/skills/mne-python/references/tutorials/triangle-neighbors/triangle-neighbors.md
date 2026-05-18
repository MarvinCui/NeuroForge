# How To: Triangle Neighbors

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test efficient vertex neighboring triangles for surfaces.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test efficient vertex neighboring triangles for surfaces.'

```python
'Test efficient vertex neighboring triangles for surfaces.'
```

**Verification:**
```python
assert all((np.array_equal(nt1, nt2) for nt1, nt2 in zip(neighbor_tri, this['neighbor_tri'])))
```

### Step 2: Assign this = value

```python
this = read_source_spaces(fname)[0]
```

### Step 3: Assign unknown = value

```python
this['neighbor_tri'] = [list() for _ in range(this['np'])]
```

### Step 4: Assign unknown = value

```python
this['neighbor_tri'] = [np.array(nb, int) for nb in this['neighbor_tri']]
```

### Step 5: Assign neighbor_tri = _triangle_neighbors(...)

```python
neighbor_tri = _triangle_neighbors(this['tris'], this['np'])
```

**Verification:**
```python
assert all((np.array_equal(nt1, nt2) for nt1, nt2 in zip(neighbor_tri, this['neighbor_tri'])))
```

### Step 6: Assign verts = value

```python
verts = this['tris'][p]
```

### Step 7: Call unknown.append()

```python
this['neighbor_tri'][verts[0]].append(p)
```

### Step 8: Call unknown.append()

```python
this['neighbor_tri'][verts[1]].append(p)
```

### Step 9: Call unknown.append()

```python
this['neighbor_tri'][verts[2]].append(p)
```


## Complete Example

```python
# Workflow
'Test efficient vertex neighboring triangles for surfaces.'
this = read_source_spaces(fname)[0]
this['neighbor_tri'] = [list() for _ in range(this['np'])]
for p in range(this['ntri']):
    verts = this['tris'][p]
    this['neighbor_tri'][verts[0]].append(p)
    this['neighbor_tri'][verts[1]].append(p)
    this['neighbor_tri'][verts[2]].append(p)
this['neighbor_tri'] = [np.array(nb, int) for nb in this['neighbor_tri']]
neighbor_tri = _triangle_neighbors(this['tris'], this['np'])
assert all((np.array_equal(nt1, nt2) for nt1, nt2 in zip(neighbor_tri, this['neighbor_tri'])))
```

## Next Steps


---

*Source: test_source_space.py:442 | Complexity: Advanced | Last updated: 2026-05-18*