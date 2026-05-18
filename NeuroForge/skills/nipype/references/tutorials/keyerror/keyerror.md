# How To: Keyerror

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test keyerror

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
# Fixtures: creating_graphs
```

## Step-by-Step Guide

### Step 1: Assign graphlist = creating_graphs

```python
graphlist = creating_graphs
```

**Verification:**
```python
assert 'the graph edges do not have Your_edge attribute' in str(e.value)
```

### Step 2: Assign group1 = value

```python
group1 = graphlist[:3]
```

### Step 3: Assign group2 = value

```python
group2 = graphlist[3:]
```

### Step 4: Assign nbs = NetworkBasedStatistic(...)

```python
nbs = NetworkBasedStatistic()
```

### Step 5: Assign nbs.inputs.in_group1 = group1

```python
nbs.inputs.in_group1 = group1
```

### Step 6: Assign nbs.inputs.in_group2 = group2

```python
nbs.inputs.in_group2 = group2
```

### Step 7: Assign nbs.inputs.edge_key = 'Your_edge'

```python
nbs.inputs.edge_key = 'Your_edge'
```

**Verification:**
```python
assert 'the graph edges do not have Your_edge attribute' in str(e.value)
```

### Step 8: Call nbs.run()

```python
nbs.run()
```


## Complete Example

```python
# Setup
# Fixtures: creating_graphs

# Workflow
graphlist = creating_graphs
group1 = graphlist[:3]
group2 = graphlist[3:]
nbs = NetworkBasedStatistic()
nbs.inputs.in_group1 = group1
nbs.inputs.in_group2 = group2
nbs.inputs.edge_key = 'Your_edge'
with pytest.raises(KeyError) as e:
    nbs.run()
assert 'the graph edges do not have Your_edge attribute' in str(e.value)
```

## Next Steps


---

*Source: test_nbs.py:47 | Complexity: Advanced | Last updated: 2026-05-18*