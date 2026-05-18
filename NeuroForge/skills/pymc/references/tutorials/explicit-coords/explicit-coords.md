# How To: Explicit Coords

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test explicit coords

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`

**Setup Required:**
```python
# Fixtures: seeded_test
```

## Step-by-Step Guide

### Step 1: Assign N_rows = 5

```python
N_rows = 5
```

**Verification:**
```python
assert 'rows' in pmodel.coords
```

### Step 2: Assign N_cols = 7

```python
N_cols = 7
```

**Verification:**
```python
assert pmodel.coords['rows'] == ('R1', 'R2', 'R3', 'R4', 'R5')
```

### Step 3: Assign data = np.random.uniform(...)

```python
data = np.random.uniform(size=(N_rows, N_cols))
```

**Verification:**
```python
assert 'rows' in pmodel.dim_lengths
```

### Step 4: Assign coords = value

```python
coords = {'rows': [f'R{r + 1}' for r in range(N_rows)], 'columns': [f'C{c + 1}' for c in range(N_cols)]}
```

**Verification:**
```python
assert pmodel.dim_lengths['rows'].eval() == 5
```

### Step 5: Call pm.Data()

```python
pm.Data('observations', data, dims=('rows', 'columns'))
```

**Verification:**
```python
assert 'columns' in pmodel.coords
```

### Step 6: Call pm.set_data()

```python
pm.set_data({'observations': data + 1})
```

**Verification:**
```python
assert pmodel.coords['columns'] == ('C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7')
```

### Step 7: Call pm.set_data()

```python
pm.set_data({'observations': data}, coords=coords)
```

**Verification:**
```python
assert pmodel.named_vars_to_dims == {'observations': ('rows', 'columns')}
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
N_rows = 5
N_cols = 7
data = np.random.uniform(size=(N_rows, N_cols))
coords = {'rows': [f'R{r + 1}' for r in range(N_rows)], 'columns': [f'C{c + 1}' for c in range(N_cols)]}
with pm.Model(coords=coords) as pmodel:
    pm.Data('observations', data, dims=('rows', 'columns'))
    pm.set_data({'observations': data + 1})
    pm.set_data({'observations': data}, coords=coords)
assert 'rows' in pmodel.coords
assert pmodel.coords['rows'] == ('R1', 'R2', 'R3', 'R4', 'R5')
assert 'rows' in pmodel.dim_lengths
assert pmodel.dim_lengths['rows'].eval() == 5
assert 'columns' in pmodel.coords
assert pmodel.coords['columns'] == ('C1', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7')
assert pmodel.named_vars_to_dims == {'observations': ('rows', 'columns')}
assert 'columns' in pmodel.dim_lengths
assert pmodel.dim_lengths['columns'].eval() == 7
```

## Next Steps


---

*Source: test_data.py:314 | Complexity: Intermediate | Last updated: 2026-05-18*