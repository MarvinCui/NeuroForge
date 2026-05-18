# How To: Iap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test iap

## Prerequisites

**Required Modules:**
- `pathlib`
- `sys`
- `tempfile`
- `numpy.testing`
- `dipy.workflows.base`
- `dipy.workflows.flow_runner`
- `dipy.workflows.tests.workflow_tests_utils`


## Step-by-Step Guide

### Step 1: Assign sys.argv = value

```python
sys.argv = [sys.argv[0]]
```

### Step 2: Assign pos_keys = value

```python
pos_keys = ['positional_str', 'positional_bool', 'positional_int', 'positional_float']
```

### Step 3: Assign opt_keys = value

```python
opt_keys = ['optional_str', 'optional_bool', 'optional_int', 'optional_float', 'optional_int_2', 'optional_float_2']
```

### Step 4: Assign pos_results = value

```python
pos_results = ['test', 0, 10, 10.2]
```

### Step 5: Assign opt_results = value

```python
opt_results = ['opt_test', True, 20, 20.2, None, None]
```

### Step 6: Assign inputs = inputs_from_results(...)

```python
inputs = inputs_from_results(opt_results, opt_keys, optional=True)
```

### Step 7: Call inputs.extend()

```python
inputs.extend(inputs_from_results(pos_results))
```

### Step 8: Call sys.argv.extend()

```python
sys.argv.extend(inputs)
```

### Step 9: Assign parser = IntrospectiveArgumentParser(...)

```python
parser = IntrospectiveArgumentParser()
```

### Step 10: Assign dummy_flow = DummyFlow(...)

```python
dummy_flow = DummyFlow()
```

### Step 11: Call parser.add_workflow()

```python
parser.add_workflow(dummy_flow)
```

### Step 12: Assign args = parser.get_flow_args(...)

```python
args = parser.get_flow_args()
```

### Step 13: Assign all_keys = value

```python
all_keys = pos_keys + opt_keys
```

### Step 14: Assign all_results = value

```python
all_results = pos_results + opt_results
```

### Step 15: Assign return_values = dummy_flow.run(...)

```python
return_values = dummy_flow.run(**args)
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(return_values, all_results + [2.0])
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(args[k], v)
```


## Complete Example

```python
# Workflow
sys.argv = [sys.argv[0]]
pos_keys = ['positional_str', 'positional_bool', 'positional_int', 'positional_float']
opt_keys = ['optional_str', 'optional_bool', 'optional_int', 'optional_float', 'optional_int_2', 'optional_float_2']
pos_results = ['test', 0, 10, 10.2]
opt_results = ['opt_test', True, 20, 20.2, None, None]
inputs = inputs_from_results(opt_results, opt_keys, optional=True)
inputs.extend(inputs_from_results(pos_results))
sys.argv.extend(inputs)
parser = IntrospectiveArgumentParser()
dummy_flow = DummyFlow()
parser.add_workflow(dummy_flow)
args = parser.get_flow_args()
all_keys = pos_keys + opt_keys
all_results = pos_results + opt_results
for k, v in zip(all_keys, all_results):
    npt.assert_equal(args[k], v)
return_values = dummy_flow.run(**args)
npt.assert_array_equal(return_values, all_results + [2.0])
```

## Next Steps


---

*Source: test_iap.py:82 | Complexity: Advanced | Last updated: 2026-05-18*