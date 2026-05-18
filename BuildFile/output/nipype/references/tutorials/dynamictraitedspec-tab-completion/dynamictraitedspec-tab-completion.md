# How To: Dynamictraitedspec Tab Completion

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test DynamicTraitedSpec tab completion

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

### Step 1: Assign func_interface = Function(...)

```python
func_interface = Function(input_names=['list_out'], output_names=['out_file', 'another_file'], function=extract_func)
```

**Verification:**
```python
assert set(func_interface.inputs.__all__) == expected_input
```

### Step 2: Assign list_extract = Node(...)

```python
list_extract = Node(Function(input_names=['list_out'], output_names=['out_file'], function=extract_func), name='list_extract')
```

**Verification:**
```python
assert set(list_extract.inputs.__all__) == expected_input
```

### Step 3: Assign expected_input = set(...)

```python
expected_input = set(list_extract.inputs.editable_traits())
```

**Verification:**
```python
assert set(list_extract.outputs.__all__) == expected_output
```

### Step 4: Assign expected_output = set(...)

```python
expected_output = set(list_extract.outputs.editable_traits())
```

**Verification:**
```python
assert set(list_extract.outputs.__all__) == expected_output
```

### Step 5: Call list_extract._interface._output_names.append()

```python
list_extract._interface._output_names.append('added_out_trait')
```

### Step 6: Call expected_output.add()

```python
expected_output.add('added_out_trait')
```

**Verification:**
```python
assert set(list_extract.outputs.__all__) == expected_output
```


## Complete Example

```python
# Workflow
def extract_func(list_out):
    return list_out[0]
func_interface = Function(input_names=['list_out'], output_names=['out_file', 'another_file'], function=extract_func)
list_extract = Node(Function(input_names=['list_out'], output_names=['out_file'], function=extract_func), name='list_extract')
expected_input = set(list_extract.inputs.editable_traits())
assert set(func_interface.inputs.__all__) == expected_input
assert set(list_extract.inputs.__all__) == expected_input
expected_output = set(list_extract.outputs.editable_traits())
assert set(list_extract.outputs.__all__) == expected_output
list_extract._interface._output_names.append('added_out_trait')
expected_output.add('added_out_trait')
assert set(list_extract.outputs.__all__) == expected_output
```

## Next Steps


---

*Source: test_specs.py:82 | Complexity: Intermediate | Last updated: 2026-05-18*