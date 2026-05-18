# How To: Mapnode Iterfield Check

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapnode iterfield check

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign mod1 = pe.MapNode(...)

```python
mod1 = pe.MapNode(EngineTestInterface(), iterfield=['input1'], name='mod1')
```

### Step 2: Assign mod1 = pe.MapNode(...)

```python
mod1 = pe.MapNode(EngineTestInterface(), iterfield=['input1', 'input2'], name='mod1')
```

### Step 3: Assign mod1.inputs.input1 = value

```python
mod1.inputs.input1 = [1, 2]
```

### Step 4: Assign mod1.inputs.input2 = 3

```python
mod1.inputs.input2 = 3
```

### Step 5: Call mod1._check_iterfield()

```python
mod1._check_iterfield()
```

### Step 6: Call mod1._check_iterfield()

```python
mod1._check_iterfield()
```


## Complete Example

```python
# Workflow
mod1 = pe.MapNode(EngineTestInterface(), iterfield=['input1'], name='mod1')
with pytest.raises(ValueError):
    mod1._check_iterfield()
mod1 = pe.MapNode(EngineTestInterface(), iterfield=['input1', 'input2'], name='mod1')
mod1.inputs.input1 = [1, 2]
mod1.inputs.input2 = 3
with pytest.raises(ValueError):
    mod1._check_iterfield()
```

## Next Steps


---

*Source: test_nodes.py:103 | Complexity: Intermediate | Last updated: 2026-05-18*