# How To: Traitedspec Tab Completion

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TraitedSpec tab completion

## Prerequisites

**Required Modules:**
- `os`
- `warnings`
- `pytest`
- `utils.filemanip`
- `base`
- `interfaces`
- `utility.wrappers`
- `pipeline`
- `specs`
- `pickle`


## Step-by-Step Guide

### Step 1: Assign bet_nd = Node(...)

```python
bet_nd = Node(fsl.BET(), name='bet')
```

**Verification:**
```python
assert set(bet_nd.inputs.__all__) == set(bet_inputs)
```

### Step 2: Assign bet_interface = fsl.BET(...)

```python
bet_interface = fsl.BET()
```

**Verification:**
```python
assert set(bet_interface.inputs.__all__) == set(bet_inputs)
```

### Step 3: Assign bet_inputs = bet_nd.inputs.class_editable_traits(...)

```python
bet_inputs = bet_nd.inputs.class_editable_traits()
```

**Verification:**
```python
assert set(bet_nd.outputs.__all__) == set(bet_outputs)
```

### Step 4: Assign bet_outputs = bet_nd.outputs.class_editable_traits(...)

```python
bet_outputs = bet_nd.outputs.class_editable_traits()
```

**Verification:**
```python
assert set(bet_nd.inputs.__all__) == set(bet_inputs)
```


## Complete Example

```python
# Workflow
bet_nd = Node(fsl.BET(), name='bet')
bet_interface = fsl.BET()
bet_inputs = bet_nd.inputs.class_editable_traits()
bet_outputs = bet_nd.outputs.class_editable_traits()
assert set(bet_nd.inputs.__all__) == set(bet_inputs)
assert set(bet_interface.inputs.__all__) == set(bet_inputs)
assert set(bet_nd.outputs.__all__) == set(bet_outputs)
```

## Next Steps


---

*Source: test_specs.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*