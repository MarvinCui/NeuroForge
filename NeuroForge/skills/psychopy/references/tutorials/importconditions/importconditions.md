# How To: Importconditions

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate OrderedDict: test importConditions

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.data`
- `os.path`
- `numpy`
- `numpy`
- `time`


## Step-by-Step Guide

### Step 1: Assign expected_cond = utils.OrderedDict(...)

```python
expected_cond = utils.OrderedDict([('text', 'red'), ('congruent', 1), ('corrAns', 1), ('letterColor', 'red'), ('n', 2), ('float', 1.1)])
```


## Complete Example

```python
# Workflow
expected_cond = utils.OrderedDict([('text', 'red'), ('congruent', 1), ('corrAns', 1), ('letterColor', 'red'), ('n', 2), ('float', 1.1)])
```

## Next Steps


---

*Source: test_utils.py:29 | Complexity: Beginner | Last updated: 2026-05-18*