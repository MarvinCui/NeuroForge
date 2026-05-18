# How To: Importerror

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test importerror

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nbs`
- `utils.misc`
- `numpy`
- `networkx`
- `pickle`
- `pytest`

**Setup Required:**
```python
# Fixtures: creating_graphs, tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign graphlist = creating_graphs

```python
graphlist = creating_graphs
```

### Step 3: Assign group1 = value

```python
group1 = graphlist[:3]
```

### Step 4: Assign group2 = value

```python
group2 = graphlist[3:]
```

### Step 5: Assign nbs = NetworkBasedStatistic(...)

```python
nbs = NetworkBasedStatistic()
```

### Step 6: Assign nbs.inputs.in_group1 = group1

```python
nbs.inputs.in_group1 = group1
```

### Step 7: Assign nbs.inputs.in_group2 = group2

```python
nbs.inputs.in_group2 = group2
```

### Step 8: Assign nbs.inputs.edge_key = 'weight'

```python
nbs.inputs.edge_key = 'weight'
```

### Step 9: Call nbs.run()

```python
nbs.run()
```


## Complete Example

```python
# Setup
# Fixtures: creating_graphs, tmpdir

# Workflow
tmpdir.chdir()
graphlist = creating_graphs
group1 = graphlist[:3]
group2 = graphlist[3:]
nbs = NetworkBasedStatistic()
nbs.inputs.in_group1 = group1
nbs.inputs.in_group2 = group2
nbs.inputs.edge_key = 'weight'
with pytest.raises(ImportError):
    nbs.run()
```

## Next Steps


---

*Source: test_nbs.py:31 | Complexity: Advanced | Last updated: 2026-05-18*