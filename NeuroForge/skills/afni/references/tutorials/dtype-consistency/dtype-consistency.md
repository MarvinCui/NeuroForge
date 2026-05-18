# How To: Dtype Consistency

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dtype consistency

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `__future__`
- `py.test`
- `inspect`
- `mdp`
- `_tools`

**Setup Required:**
```python
# Fixtures: klass, init_args, inp_arg_gen, sup_arg_gen, execute_arg_gen
```

## Step-by-Step Guide

### Step 1: Assign args = call_init_args(...)

```python
args = call_init_args(init_args)
```

**Verification:**
```python
assert out.dtype == dtype
```

### Step 2: Assign supported_types = klass.get_supported_dtypes(...)

```python
supported_types = klass(*args).get_supported_dtypes()
```

### Step 3: Assign inp = inp_arg_gen(...)

```python
inp = inp_arg_gen()
```

### Step 4: Assign args = call_init_args(...)

```python
args = call_init_args(init_args)
```

### Step 5: Assign node = klass(...)

```python
node = klass(*args, dtype=dtype)
```

### Step 6: Call _train_if_necessary()

```python
_train_if_necessary(inp, node, sup_arg_gen)
```

### Step 7: Assign extra = value

```python
extra = [execute_arg_gen(inp)] if execute_arg_gen else []
```

**Verification:**
```python
assert out.dtype == dtype
```

### Step 8: Assign out = node.execute(...)

```python
out = node.execute(inp, *extra)
```

### Step 9: Assign out = node.execute(...)

```python
out = node.execute(x, *extra)
```


## Complete Example

```python
# Setup
# Fixtures: klass, init_args, inp_arg_gen, sup_arg_gen, execute_arg_gen

# Workflow
args = call_init_args(init_args)
supported_types = klass(*args).get_supported_dtypes()
for dtype in supported_types:
    inp = inp_arg_gen()
    args = call_init_args(init_args)
    node = klass(*args, dtype=dtype)
    _train_if_necessary(inp, node, sup_arg_gen)
    extra = [execute_arg_gen(inp)] if execute_arg_gen else []
    if isinstance(inp, Iter):
        for x in inp:
            out = node.execute(x, *extra)
    else:
        out = node.execute(inp, *extra)
    assert out.dtype == dtype
```

## Next Steps


---

*Source: test_nodes_generic.py:150 | Complexity: Advanced | Last updated: 2026-05-18*