# How To: Itersource Expansion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test itersource expansion

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign wf1 = pe.Workflow(...)

```python
wf1 = pe.Workflow(name='test')
```

**Verification:**
```python
assert len(pe.generate_expanded_graph(wf3._flatgraph).nodes()) == 42
```

### Step 2: Assign node1 = pe.Node(...)

```python
node1 = pe.Node(EngineTestInterface(), name='node1')
```

### Step 3: Assign node1.iterables = value

```python
node1.iterables = ('input1', [1, 2])
```

### Step 4: Assign node2 = pe.Node(...)

```python
node2 = pe.Node(EngineTestInterface(), name='node2')
```

### Step 5: Call wf1.connect()

```python
wf1.connect(node1, 'output1', node2, 'input1')
```

### Step 6: Assign node3 = pe.Node(...)

```python
node3 = pe.Node(EngineTestInterface(), name='node3')
```

### Step 7: Assign node3.itersource = value

```python
node3.itersource = ('node1', 'input1')
```

### Step 8: Assign node3.iterables = value

```python
node3.iterables = [('input1', {1: [3, 4], 2: [5, 6, 7]})]
```

### Step 9: Call wf1.connect()

```python
wf1.connect(node2, 'output1', node3, 'input1')
```

### Step 10: Assign node4 = pe.Node(...)

```python
node4 = pe.Node(EngineTestInterface(), name='node4')
```

### Step 11: Call wf1.connect()

```python
wf1.connect(node3, 'output1', node4, 'input1')
```

### Step 12: Assign wf3 = pe.Workflow(...)

```python
wf3 = pe.Workflow(name='group')
```

### Step 13: Assign wf3._flatgraph = wf3._create_flat_graph(...)

```python
wf3._flatgraph = wf3._create_flat_graph()
```

**Verification:**
```python
assert len(pe.generate_expanded_graph(wf3._flatgraph).nodes()) == 42
```

### Step 14: Call wf3.add_nodes()

```python
wf3.add_nodes([wf1.clone(name='test%d' % i)])
```


## Complete Example

```python
# Workflow
wf1 = pe.Workflow(name='test')
node1 = pe.Node(EngineTestInterface(), name='node1')
node1.iterables = ('input1', [1, 2])
node2 = pe.Node(EngineTestInterface(), name='node2')
wf1.connect(node1, 'output1', node2, 'input1')
node3 = pe.Node(EngineTestInterface(), name='node3')
node3.itersource = ('node1', 'input1')
node3.iterables = [('input1', {1: [3, 4], 2: [5, 6, 7]})]
wf1.connect(node2, 'output1', node3, 'input1')
node4 = pe.Node(EngineTestInterface(), name='node4')
wf1.connect(node3, 'output1', node4, 'input1')
wf3 = pe.Workflow(name='group')
for i in [0, 1, 2]:
    wf3.add_nodes([wf1.clone(name='test%d' % i)])
wf3._flatgraph = wf3._create_flat_graph()
assert len(pe.generate_expanded_graph(wf3._flatgraph).nodes()) == 42
```

## Next Steps


---

*Source: test_engine.py:197 | Complexity: Advanced | Last updated: 2026-05-18*