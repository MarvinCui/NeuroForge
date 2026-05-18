# How To: Processorcounts

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test processorCounts

## Prerequisites

**Required Modules:**
- `psychopy.tests`
- `psychopy.tests.test_iohub.testutil`
- `psychopy.iohub`
- `psychopy.core`


## Step-by-Step Guide

### Step 1: Assign get_puc = Computer.getProcessingUnitCount(...)

```python
get_puc = Computer.getProcessingUnitCount()
```

**Verification:**
```python
assert puc == get_puc
```

### Step 2: Assign cc = value

```python
cc = Computer.core_count
```

**Verification:**
```python
assert type(cc) is int
```

### Step 3: Assign puc = value

```python
puc = Computer.processing_unit_count
```

**Verification:**
```python
assert type(puc) is int
```


## Complete Example

```python
# Workflow
get_puc = Computer.getProcessingUnitCount()
cc = Computer.core_count
puc = Computer.processing_unit_count
assert puc == get_puc
assert type(cc) is int
assert type(puc) is int
assert puc > 0
assert cc > 0
assert cc <= puc
```

## Next Steps


---

*Source: test_computer.py:59 | Complexity: Beginner | Last updated: 2026-05-18*