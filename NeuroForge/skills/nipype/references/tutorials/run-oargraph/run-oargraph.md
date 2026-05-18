# How To: Run Oargraph

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test run oargraph

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `nipype.interfaces.base`
- `pytest`
- `nipype.pipeline.engine`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign pipe = pe.Workflow(...)

```python
pipe = pe.Workflow(name='pipe', base_dir=str(tmp_path))
```

**Verification:**
```python
assert result == [1, 1]
```

### Step 2: Assign mod1 = pe.Node(...)

```python
mod1 = pe.Node(interface=OarTestInterface(), name='mod1')
```

### Step 3: Assign mod2 = pe.MapNode(...)

```python
mod2 = pe.MapNode(interface=OarTestInterface(), iterfield=['input1'], name='mod2')
```

### Step 4: Call pipe.connect()

```python
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
```

### Step 5: Assign pipe.base_dir = os.getcwd(...)

```python
pipe.base_dir = os.getcwd()
```

### Step 6: Assign mod1.inputs.input1 = 1

```python
mod1.inputs.input1 = 1
```

### Step 7: Assign execgraph = pipe.run(...)

```python
execgraph = pipe.run(plugin='OAR')
```

### Step 8: Assign names = value

```python
names = [f'{node._hierarchy}.{node.name}' for node in execgraph.nodes()]
```

### Step 9: Assign node = value

```python
node = list(execgraph.nodes())[names.index('pipe.mod1')]
```

### Step 10: Assign result = node.get_output(...)

```python
result = node.get_output('output1')
```

**Verification:**
```python
assert result == [1, 1]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
pipe = pe.Workflow(name='pipe', base_dir=str(tmp_path))
mod1 = pe.Node(interface=OarTestInterface(), name='mod1')
mod2 = pe.MapNode(interface=OarTestInterface(), iterfield=['input1'], name='mod2')
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
pipe.base_dir = os.getcwd()
mod1.inputs.input1 = 1
execgraph = pipe.run(plugin='OAR')
names = [f'{node._hierarchy}.{node.name}' for node in execgraph.nodes()]
node = list(execgraph.nodes())[names.index('pipe.mod1')]
result = node.get_output('output1')
assert result == [1, 1]
```

## Next Steps


---

*Source: test_oar.py:34 | Complexity: Advanced | Last updated: 2026-05-18*