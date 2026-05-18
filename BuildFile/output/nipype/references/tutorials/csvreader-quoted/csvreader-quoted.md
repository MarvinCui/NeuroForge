# How To: Csvreader Quoted

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test csvReader quoted

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign lines = value

```python
lines = ['foo,"hello, world",300.1\n']
```

**Verification:**
```python
assert out.outputs.column_0 == ['foo']
```

### Step 2: Assign name = value

```python
name = tmpdir.join('testfile.csv').strpath
```

**Verification:**
```python
assert out.outputs.column_1 == ['hello, world']
```

### Step 3: Assign reader = utility.CSVReader(...)

```python
reader = utility.CSVReader()
```

**Verification:**
```python
assert out.outputs.column_2 == ['300.1']
```

### Step 4: Call fid.writelines()

```python
fid.writelines(lines)
```

### Step 5: Call fid.flush()

```python
fid.flush()
```

### Step 6: Assign reader.inputs.in_file = name

```python
reader.inputs.in_file = name
```

### Step 7: Assign out = reader.run(...)

```python
out = reader.run()
```

**Verification:**
```python
assert out.outputs.column_0 == ['foo']
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
lines = ['foo,"hello, world",300.1\n']
name = tmpdir.join('testfile.csv').strpath
with open(name, 'w') as fid:
    reader = utility.CSVReader()
    fid.writelines(lines)
    fid.flush()
    reader.inputs.in_file = name
    out = reader.run()
    assert out.outputs.column_0 == ['foo']
    assert out.outputs.column_1 == ['hello, world']
    assert out.outputs.column_2 == ['300.1']
```

## Next Steps


---

*Source: test_csv.py:31 | Complexity: Intermediate | Last updated: 2026-05-18*