# How To: Data Var Latex Underscore Escaping

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Data variable names with underscores are escaped in LaTeX (direct call and model repr).

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor.tensor.random`
- `rich.console`
- `rich.table`
- `pymc`
- `pymc`
- `pymc.distributions`
- `pymc.math`
- `pymc.model`
- `pymc.printing`
- `pymc.pytensorf`
- `pymc.printing`
- `pymc.dims.distributions`
- `pymc.dims.distributions`
- `pymc`

**Required Fixtures:**
- `api_client` fixture


## Step-by-Step Guide

### Step 1: 'Data variable names with underscores are escaped in LaTeX (direct call and model repr).'

```python
'Data variable names with underscores are escaped in LaTeX (direct call and model repr).'
```

**Verification:**
```python
assert 'my\\_data' in latex_with_params
```

### Step 2: Assign latex_with_params = str_for_data_var(...)

```python
latex_with_params = str_for_data_var(my_data, formatting='latex', include_params=True)
```

**Verification:**
```python
assert '\\operatorname{Data}(42)' in latex_with_params
```

### Step 3: Assign latex_no_params = str_for_data_var(...)

```python
latex_no_params = str_for_data_var(my_data, formatting='latex', include_params=False)
```

**Verification:**
```python
assert 'my\\_data' in latex_no_params
```

### Step 4: Assign model_latex = model.str_repr(...)

```python
model_latex = model.str_repr(formatting='latex')
```

**Verification:**
```python
assert '\\operatorname{Data}' in latex_no_params
```

### Step 5: Assign my_data = Data(...)

```python
my_data = Data('my_data', 42)
```

**Verification:**
```python
assert 'my\\_data' in model_latex
```

### Step 6: Call Normal()

```python
Normal('y', my_data)
```


## Complete Example

```python
# Workflow
'Data variable names with underscores are escaped in LaTeX (direct call and model repr).'
from pymc.printing import str_for_data_var
with Model() as model:
    my_data = Data('my_data', 42)
    Normal('y', my_data)
latex_with_params = str_for_data_var(my_data, formatting='latex', include_params=True)
assert 'my\\_data' in latex_with_params
assert '\\operatorname{Data}(42)' in latex_with_params
latex_no_params = str_for_data_var(my_data, formatting='latex', include_params=False)
assert 'my\\_data' in latex_no_params
assert '\\operatorname{Data}' in latex_no_params
model_latex = model.str_repr(formatting='latex')
assert 'my\\_data' in model_latex
```

## Next Steps


---

*Source: test_printing.py:428 | Complexity: Intermediate | Last updated: 2026-05-18*