# How To: Aliasdict

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the AliasDict class works as expected.

## Prerequisites

**Required Modules:**
- `psychopy.tools`
- `pytest`
- `numpy`


## Step-by-Step Guide

### Step 1: '\n    Test that the AliasDict class works as expected.\n    '

```python
'\n    Test that the AliasDict class works as expected.\n    '
```

**Verification:**
```python
assert 'participant' in params
```

### Step 2: Assign params = at.AliasDict(...)

```python
params = at.AliasDict({'patient': 1})
```

**Verification:**
```python
assert key != 'participant'
```

### Step 3: Call params.alias()

```python
params.alias('patient', alias='participant')
```

**Verification:**
```python
assert params['patient'] == params['participant'] == 1
```

### Step 4: Assign unknown = 2

```python
params['participant'] = 2
```

**Verification:**
```python
assert params['patient'] == params['participant'] == 2
```

### Step 5: Assign unknown = 3

```python
params['patient'] = 3
```

**Verification:**
```python
assert params['patient'] == params['participant'] == 3
```

### Step 6: Assign params2 = at.AliasDict(...)

```python
params2 = at.AliasDict({'1': 1})
```

**Verification:**
```python
assert 'one' not in params.aliases
```

### Step 7: Call params2.alias()

```python
params2.alias('1', alias='one')
```

**Verification:**
```python
assert '1' not in params.aliases
```


## Complete Example

```python
# Workflow
'\n    Test that the AliasDict class works as expected.\n    '
params = at.AliasDict({'patient': 1})
params.alias('patient', alias='participant')
assert 'participant' in params
for key in params:
    assert key != 'participant'
assert params['patient'] == params['participant'] == 1
params['participant'] = 2
assert params['patient'] == params['participant'] == 2
params['patient'] = 3
assert params['patient'] == params['participant'] == 3
params2 = at.AliasDict({'1': 1})
params2.alias('1', alias='one')
assert 'one' not in params.aliases
assert '1' not in params.aliases
```

## Next Steps


---

*Source: test_arraytools.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*