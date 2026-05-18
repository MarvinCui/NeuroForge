# How To: Mapnode Single

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mapnode single

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `test_base`
- `test_utils`
- `nipype`
- `nipype`
- `nipype`
- `nipype.interfaces.utility`
- `nipype.pipeline.plugins.base`
- `stat`
- `os`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign pnode = pe.MapNode(...)

```python
pnode = pe.MapNode(niu.Function(function=_producer), name='ProducerNode', iterfield=['num'])
```

### Step 3: Assign pnode.inputs.num = value

```python
pnode.inputs.num = [7]
```

### Step 4: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='PC_Workflow')
```

### Step 5: Call wf.add_nodes()

```python
wf.add_nodes([pnode])
```

### Step 6: Assign wf.base_dir = os.path.abspath(...)

```python
wf.base_dir = os.path.abspath('./test_output')
```

### Step 7: Call wf.run()

```python
wf.run(plugin='MultiProc')
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()

def _producer(num=1, deadly_num=7):
    if num == deadly_num:
        raise RuntimeError('Got the deadly num (%d).' % num)
    return num + 1
pnode = pe.MapNode(niu.Function(function=_producer), name='ProducerNode', iterfield=['num'])
pnode.inputs.num = [7]
wf = pe.Workflow(name='PC_Workflow')
wf.add_nodes([pnode])
wf.base_dir = os.path.abspath('./test_output')
with pytest.raises(RuntimeError):
    wf.run(plugin='MultiProc')
```

## Next Steps


---

*Source: test_nodes.py:320 | Complexity: Intermediate | Last updated: 2026-05-18*