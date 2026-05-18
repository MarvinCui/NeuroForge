# How To: 2Mods

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 2mods

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

### Step 3: Assign mod2 = pe.Node(...)

```python
mod2 = pe.Node(interface=EngineTestInterface(), name='mod2')
```

### Step 4: Call pipe.connect()

```python
pipe.connect([(mod1, mod2, [('output1', 'input2')])])
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

### Step 7: Assign eval.iterables = value

```python
eval('mod' + nr).iterables = iterables[nr]
```


## Complete Example

```python
# Setup
# Fixtures: iterables, expected

# Workflow
pipe = pe.Workflow(name='pipe')
mod1 = pe.Node(interface=EngineTestInterface(), name='mod1')
mod2 = pe.Node(interface=EngineTestInterface(), name='mod2')
for nr in ['1', '2']:
    eval('mod' + nr).iterables = iterables[nr]
pipe.connect([(mod1, mod2, [('output1', 'input2')])])
pipe._flatgraph = pipe._create_flat_graph()
pipe._execgraph = pe.generate_expanded_graph(deepcopy(pipe._flatgraph))
assert len(pipe._execgraph.nodes()) == expected[0]
assert len(pipe._execgraph.edges()) == expected[1]
```

## Next Steps


---

*Source: test_engine.py:47 | Complexity: Intermediate | Last updated: 2026-05-18*