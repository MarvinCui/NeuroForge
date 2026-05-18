# How To: Unique Join Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test join with the ``unique`` flag set to True.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `interfaces`
- `interfaces.utility`
- `interfaces.base`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test join with the ``unique`` flag set to True.'

```python
'Test join with the ``unique`` flag set to True.'
```

**Verification:**
```python
assert _sum_operands[0] == [4, 2, 3], 'The unique join output value is incorrect: %s.' % _sum_operands[0]
```

### Step 2: Assign _sum_operands = value

```python
_sum_operands = []
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 4: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 5: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 6: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [3, 1, 2, 1, 3])]
```

### Step 7: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 8: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 9: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(SumInterface(), joinsource='inputspec', joinfield='input1', unique=True, name='join')
```

### Step 10: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', join, 'input1')
```

### Step 11: Call wf.run()

```python
wf.run()
```

**Verification:**
```python
assert _sum_operands[0] == [4, 2, 3], 'The unique join output value is incorrect: %s.' % _sum_operands[0]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test join with the ``unique`` flag set to True.'
global _sum_operands
_sum_operands = []
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [3, 1, 2, 1, 3])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
join = pe.JoinNode(SumInterface(), joinsource='inputspec', joinfield='input1', unique=True, name='join')
wf.connect(pre_join1, 'output1', join, 'input1')
wf.run()
assert _sum_operands[0] == [4, 2, 3], 'The unique join output value is incorrect: %s.' % _sum_operands[0]
```

## Next Steps


---

*Source: test_join.py:246 | Complexity: Advanced | Last updated: 2026-05-18*