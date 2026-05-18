# How To: 1Mod

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 1mod

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `glob`
- `os`
- `pytest`
- `test_base`
- `nipype.interfaces.utility`
- `nipype`
- `interfaces.utility`
- `testing`
- `nipype`
- `nipype.interfaces.io`
- `nipype.interfaces.base`
- `nipype.interfaces.utility`

**Setup Required:**
```python
# Fixtures: iterables, expected
```

## Step-by-Step Guide

### Step 1: Assign pipe = pe.Workflow(...)

```python
pipe = pe.Workflow(name='pipe')
```

**Verification:**
```python
assert len(pipe._execgraph.nodes()) == expected[0]
```

### Step 2: Assign mod1 = pe.Node(...)

```python
mod1 = pe.Node(interface=EngineTestInterface(), name='mod1')
```

**Verification:**
```python
assert len(pipe._execgraph.edges()) == expected[1]
```

### Step 3: Assign mod1.iterables = value

```python
mod1.iterables = iterables['1']
```

### Step 4: Call pipe.add_nodes()

```python
pipe.add_nodes([mod1])
```

### Step 5: Assign pipe._flatgraph = pipe._create_flat_graph(...)

```python
pipe._flatgraph = pipe._create_flat_graph()
```

### Step 6: Assign pipe._execgraph = pe.generate_expanded_graph(...)

```python
pipe._execgraph = pe.generate_expanded_graph(deepcopy(pipe._flatgraph))
```

**Verification:**
```python
assert len(pipe._execgraph.nodes()) == expected[0]
```


## Complete Example

```python
# Setup
# Fixtures: iterables, expected

# Workflow
pipe = pe.Workflow(name='pipe')
mod1 = pe.Node(interface=EngineTestInterface(), name='mod1')
mod1.iterables = iterables['1']
pipe.add_nodes([mod1])
pipe._flatgraph = pipe._create_flat_graph()
pipe._execgraph = pe.generate_expanded_graph(deepcopy(pipe._flatgraph))
assert len(pipe._execgraph.nodes()) == expected[0]
assert len(pipe._execgraph.edges()) == expected[1]
```

## Next Steps


---

*Source: test_engine.py:25 | Complexity: Intermediate | Last updated: 2026-05-18*