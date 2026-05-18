# How To: Set Join Node File Input

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test collecting join inputs to a set.

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

### Step 1: 'Test collecting join inputs to a set.'

```python
'Test collecting join inputs to a set.'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 3: Call open.close()

```python
open('test.nii', 'w+').close()
```

### Step 4: Call open.close()

```python
open('test2.nii', 'w+').close()
```

### Step 5: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 6: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 7: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [tmpdir.join('test.nii').strpath, tmpdir.join('test2.nii').strpath])]
```

### Step 8: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IdentityInterface(fields=['n']), name='pre_join1')
```

### Step 9: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'n')
```

### Step 10: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(PickFirst(), joinsource='inputspec', joinfield='in_files', name='join')
```

### Step 11: Call wf.connect()

```python
wf.connect(pre_join1, 'n', join, 'in_files')
```

### Step 12: Call wf.run()

```python
wf.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test collecting join inputs to a set.'
tmpdir.chdir()
open('test.nii', 'w+').close()
open('test2.nii', 'w+').close()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [tmpdir.join('test.nii').strpath, tmpdir.join('test2.nii').strpath])]
pre_join1 = pe.Node(IdentityInterface(fields=['n']), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'n')
join = pe.JoinNode(PickFirst(), joinsource='inputspec', joinfield='in_files', name='join')
wf.connect(pre_join1, 'n', join, 'in_files')
wf.run()
```

## Next Steps


---

*Source: test_join.py:559 | Complexity: Advanced | Last updated: 2026-05-18*