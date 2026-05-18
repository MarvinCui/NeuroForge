# How To: Expansion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test expansion

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

### Step 1: Assign pipe1 = pe.Workflow(...)

```python
pipe1 = pe.Workflow(name='pipe1')
```

### Step 2: Assign mod1 = pe.Node(...)

```python
mod1 = pe.Node(interface=EngineTestInterface(), name='mod1')
```

### Step 3: Assign mod2 = pe.Node(...)

```python
mod2 = pe.Node(interface=EngineTestInterface(), name='mod2')
```

### Step 4: Call pipe1.connect()

```python
pipe1.connect([(mod1, mod2, [('output1', 'input2')])])
```

### Step 5: Assign pipe2 = pe.Workflow(...)

```python
pipe2 = pe.Workflow(name='pipe2')
```

### Step 6: Assign mod3 = pe.Node(...)

```python
mod3 = pe.Node(interface=EngineTestInterface(), name='mod3')
```

### Step 7: Assign mod4 = pe.Node(...)

```python
mod4 = pe.Node(interface=EngineTestInterface(), name='mod4')
```

### Step 8: Call pipe2.connect()

```python
pipe2.connect([(mod3, mod4, [('output1', 'input2')])])
```

### Step 9: Assign pipe3 = pe.Workflow(...)

```python
pipe3 = pe.Workflow(name='pipe3')
```

### Step 10: Call pipe3.connect()

```python
pipe3.connect([(pipe1, pipe2, [('mod2.output1', 'mod4.input1')])])
```

### Step 11: Assign pipe4 = pe.Workflow(...)

```python
pipe4 = pe.Workflow(name='pipe4')
```

### Step 12: Assign mod5 = pe.Node(...)

```python
mod5 = pe.Node(interface=EngineTestInterface(), name='mod5')
```

### Step 13: Call pipe4.add_nodes()

```python
pipe4.add_nodes([mod5])
```

### Step 14: Assign pipe5 = pe.Workflow(...)

```python
pipe5 = pe.Workflow(name='pipe5')
```

### Step 15: Call pipe5.add_nodes()

```python
pipe5.add_nodes([pipe4])
```

### Step 16: Assign pipe6 = pe.Workflow(...)

```python
pipe6 = pe.Workflow(name='pipe6')
```

### Step 17: Call pipe6.connect()

```python
pipe6.connect([(pipe5, pipe3, [('pipe4.mod5.output1', 'pipe2.mod3.input1')])])
```

### Step 18: Assign pipe6._flatgraph = pipe6._create_flat_graph(...)

```python
pipe6._flatgraph = pipe6._create_flat_graph()
```


## Complete Example

```python
# Workflow
pipe1 = pe.Workflow(name='pipe1')
mod1 = pe.Node(interface=EngineTestInterface(), name='mod1')
mod2 = pe.Node(interface=EngineTestInterface(), name='mod2')
pipe1.connect([(mod1, mod2, [('output1', 'input2')])])
pipe2 = pe.Workflow(name='pipe2')
mod3 = pe.Node(interface=EngineTestInterface(), name='mod3')
mod4 = pe.Node(interface=EngineTestInterface(), name='mod4')
pipe2.connect([(mod3, mod4, [('output1', 'input2')])])
pipe3 = pe.Workflow(name='pipe3')
pipe3.connect([(pipe1, pipe2, [('mod2.output1', 'mod4.input1')])])
pipe4 = pe.Workflow(name='pipe4')
mod5 = pe.Node(interface=EngineTestInterface(), name='mod5')
pipe4.add_nodes([mod5])
pipe5 = pe.Workflow(name='pipe5')
pipe5.add_nodes([pipe4])
pipe6 = pe.Workflow(name='pipe6')
pipe6.connect([(pipe5, pipe3, [('pipe4.mod5.output1', 'pipe2.mod3.input1')])])
pipe6._flatgraph = pipe6._create_flat_graph()
```

## Next Steps


---

*Source: test_engine.py:123 | Complexity: Advanced | Last updated: 2026-05-18*