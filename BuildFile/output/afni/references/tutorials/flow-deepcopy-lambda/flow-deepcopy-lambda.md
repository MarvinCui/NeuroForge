# How To: Flow Deepcopy Lambda

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Copying a Flow with a lambda member function
should not throw an Exception

## Prerequisites

**Required Modules:**
- `mdp`


## Step-by-Step Guide

### Step 1: 'Copying a Flow with a lambda member function\n    should not throw an Exception'

```python
'Copying a Flow with a lambda member function\n    should not throw an Exception'
```

### Step 2: Assign generic_node = mdp.Node(...)

```python
generic_node = mdp.Node()
```

### Step 3: Assign generic_node.lambda_function = value

```python
generic_node.lambda_function = lambda: 1
```

### Step 4: Assign generic_flow = mdp.Flow(...)

```python
generic_flow = mdp.Flow([generic_node])
```

### Step 5: Call generic_flow.copy()

```python
generic_flow.copy()
```


## Complete Example

```python
# Workflow
'Copying a Flow with a lambda member function\n    should not throw an Exception'
generic_node = mdp.Node()
generic_node.lambda_function = lambda: 1
generic_flow = mdp.Flow([generic_node])
generic_flow.copy()
```

## Next Steps


---

*Source: test_copying.py:10 | Complexity: Intermediate | Last updated: 2026-05-18*