# How To: Crashfile Creation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test crashfile creation

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.pipeline.plugins.base`
- `nipype.interfaces.utility`
- `nipype.pipeline.engine`
- `pytest`
- `unittest.mock`
- `subprocess`

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
assert pipe.run(plugin=sgelike_plugin)
```

### Step 2: Assign unknown = str(...)

```python
pipe.config['execution']['crashdump_dir'] = str(tmp_path)
```

**Verification:**
```python
assert len(crashfiles) == 1
```

### Step 3: Call pipe.add_nodes()

```python
pipe.add_nodes([pe.Node(interface=Function(function=crasher), name='crasher')])
```

### Step 4: Assign sgelike_plugin = SGELikeBatchManagerBase(...)

```python
sgelike_plugin = SGELikeBatchManagerBase('')
```

### Step 5: Assign crashfiles = value

```python
crashfiles = list(tmp_path.glob('crash*crasher*.pklz')) + list(tmp_path.glob('crash*crasher*.txt'))
```

**Verification:**
```python
assert len(crashfiles) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
pipe = pe.Workflow(name='pipe', base_dir=str(tmp_path))
pipe.config['execution']['crashdump_dir'] = str(tmp_path)
pipe.add_nodes([pe.Node(interface=Function(function=crasher), name='crasher')])
sgelike_plugin = SGELikeBatchManagerBase('')
with pytest.raises(RuntimeError):
    assert pipe.run(plugin=sgelike_plugin)
crashfiles = list(tmp_path.glob('crash*crasher*.pklz')) + list(tmp_path.glob('crash*crasher*.txt'))
assert len(crashfiles) == 1
```

## Next Steps


---

*Source: test_sgelike.py:25 | Complexity: Intermediate | Last updated: 2026-05-18*