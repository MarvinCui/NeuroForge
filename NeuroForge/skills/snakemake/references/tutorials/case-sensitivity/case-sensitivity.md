# How To: Case Sensitivity

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test case sensitivity of matching

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `pytest`
- `snakemake.output_index`

**Setup Required:**
```python
# Fixtures: mocker
```

## Step-by-Step Guide

### Step 1: 'Test case sensitivity of matching'

```python
'Test case sensitivity of matching'
```

**Verification:**
```python
assert rule in matches_exact
```

### Step 2: Assign rule = mocker.Mock(...)

```python
rule = mocker.Mock(products=lambda: [Mock(constant_prefix=lambda: 'Test', constant_suffix=lambda: 'TXT')])
```

**Verification:**
```python
assert rule not in matches_lower
```

### Step 3: Assign output_index = OutputIndex(...)

```python
output_index = OutputIndex([rule])
```

### Step 4: Assign matches_exact = output_index.match(...)

```python
matches_exact = output_index.match('Test.TXT')
```

### Step 5: Assign matches_lower = output_index.match(...)

```python
matches_lower = output_index.match('test.txt')
```

**Verification:**
```python
assert rule in matches_exact
```


## Complete Example

```python
# Setup
# Fixtures: mocker

# Workflow
'Test case sensitivity of matching'
rule = mocker.Mock(products=lambda: [Mock(constant_prefix=lambda: 'Test', constant_suffix=lambda: 'TXT')])
output_index = OutputIndex([rule])
matches_exact = output_index.match('Test.TXT')
matches_lower = output_index.match('test.txt')
assert rule in matches_exact
assert rule not in matches_lower
```

## Next Steps


---

*Source: test_output_index.py:121 | Complexity: Intermediate | Last updated: 2026-05-18*