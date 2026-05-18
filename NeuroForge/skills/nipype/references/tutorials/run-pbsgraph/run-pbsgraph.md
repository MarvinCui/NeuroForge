# How To: Run Pbsgraph

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test run pbsgraph

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
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
mod1 = pe.Node(interface=PbsTestInterface(), name='mod1')
```

### Step 3: Assign mod2 = pe.MapNode(...)

```python
mod2 = pe.MapNode(interface=PbsTestInterface(), iterfield=['input1'], name='mod2')
```

### Step 4: Call pipe.connect()

```python
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
```

### Step 5: Assign mod1.inputs.input1 = 1

```python
mod1.inputs.input1 = 1
```

### Step 6: Assign execgraph = pipe.run(...)

```python
execgraph = pipe.run(plugin='PBSGraph')
```

### Step 7: Assign names = value

```python
names = [f'{node._hierarchy}.{node.name}' for node in execgraph.nodes()]
```

### Step 8: Assign node = value

```python
node = list(execgraph.nodes())[names.index('pipe.mod1')]
```

### Step 9: Assign result = node.get_output(...)

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
mod1 = pe.Node(interface=PbsTestInterface(), name='mod1')
mod2 = pe.MapNode(interface=PbsTestInterface(), iterfield=['input1'], name='mod2')
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
mod1.inputs.input1 = 1
execgraph = pipe.run(plugin='PBSGraph')
names = [f'{node._hierarchy}.{node.name}' for node in execgraph.nodes()]
node = list(execgraph.nodes())[names.index('pipe.mod1')]
result = node.get_output('output1')
assert result == [1, 1]
```

## Next Steps


---

*Source: test_pbs.py:33 | Complexity: Advanced | Last updated: 2026-05-18*