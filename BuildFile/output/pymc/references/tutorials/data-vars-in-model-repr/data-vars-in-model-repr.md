# How To: Data Vars In Model Repr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Data variables appear in model repr and in Deterministic dependency lists (issue #7536).

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


## Step-by-Step Guide

### Step 1: 'Data variables appear in model repr and in Deterministic dependency lists (issue #7536).'

```python
'Data variables appear in model repr and in Deterministic dependency lists (issue #7536).'
```

**Verification:**
```python
assert 'x = Data(0)' in text
```

### Step 2: Assign text = model.str_repr(...)

```python
text = model.str_repr()
```

**Verification:**
```python
assert 'y ~ Normal(0, 1)' in text
```

### Step 3: Assign latex = model.str_repr(...)

```python
latex = model.str_repr(formatting='latex')
```

**Verification:**
```python
assert 'f = Deterministic(f(y, x))' in text
```

### Step 4: Assign x = Data(...)

```python
x = Data('x', 0)
```

**Verification:**
```python
assert '&= &\\operatorname{Data}(0)' in latex
```

### Step 5: Assign y = Normal(...)

```python
y = Normal('y')
```

**Verification:**
```python
assert '\\text{x}' in latex
```

### Step 6: Call Deterministic()

```python
Deterministic('f', x + y)
```


## Complete Example

```python
# Workflow
'Data variables appear in model repr and in Deterministic dependency lists (issue #7536).'
with Model() as model:
    x = Data('x', 0)
    y = Normal('y')
    Deterministic('f', x + y)
text = model.str_repr()
assert 'x = Data(0)' in text
assert 'y ~ Normal(0, 1)' in text
assert 'f = Deterministic(f(y, x))' in text
latex = model.str_repr(formatting='latex')
assert '&= &\\operatorname{Data}(0)' in latex
assert '\\text{x}' in latex
```

## Next Steps


---

*Source: test_printing.py:390 | Complexity: Intermediate | Last updated: 2026-05-18*