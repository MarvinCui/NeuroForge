# How To: Implicit Coords Dataframe

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test implicit coords dataframe

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

### Step 1: Assign pd = pytest.importorskip(...)

```python
pd = pytest.importorskip('pandas')
```

**Verification:**
```python
assert 'rows' in pmodel.coords
```

### Step 2: Assign N_rows = 5

```python
N_rows = 5
```

**Verification:**
```python
assert 'columns' in pmodel.coords
```

### Step 3: Assign N_cols = 7

```python
N_cols = 7
```

**Verification:**
```python
assert pmodel.named_vars_to_dims == {'observations': ('rows', 'columns')}
```

### Step 4: Assign df_data = pd.DataFrame(...)

```python
df_data = pd.DataFrame()
```

### Step 5: Assign df_data.index.name = 'rows'

```python
df_data.index.name = 'rows'
```

### Step 6: Assign df_data.columns.name = 'columns'

```python
df_data.columns.name = 'columns'
```

**Verification:**
```python
assert 'rows' in pmodel.coords
```

### Step 7: Assign unknown = np.random.normal(...)

```python
df_data[f'Column {c + 1}'] = np.random.normal(size=(N_rows,))
```

### Step 8: Call pm.Data()

```python
pm.Data('observations', df_data, dims=('rows', 'columns'), infer_dims_and_coords=True)
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
pd = pytest.importorskip('pandas')
N_rows = 5
N_cols = 7
df_data = pd.DataFrame()
for c in range(N_cols):
    df_data[f'Column {c + 1}'] = np.random.normal(size=(N_rows,))
df_data.index.name = 'rows'
df_data.columns.name = 'columns'
with pm.Model() as pmodel:
    pm.Data('observations', df_data, dims=('rows', 'columns'), infer_dims_and_coords=True)
assert 'rows' in pmodel.coords
assert 'columns' in pmodel.coords
assert pmodel.named_vars_to_dims == {'observations': ('rows', 'columns')}
```

## Next Steps


---

*Source: test_data.py:386 | Complexity: Advanced | Last updated: 2026-05-18*