# How To: Csvreader Tabs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test csvReader tabs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign header = 'files\tlabels\terosion\n'

```python
header = 'files\tlabels\terosion\n'
```

**Verification:**
```python
assert out.outputs.files == ['foo', 'bar', 'baz']
```

### Step 2: Assign lines = value

```python
lines = ['foo\thello\t300.1\n', 'bar\tworld\t5\n', 'baz\tgoodbye\t0.3\n']
```

**Verification:**
```python
assert out.outputs.labels == ['hello', 'world', 'goodbye']
```

### Step 3: Assign name = value

```python
name = tmpdir.join('testfile.csv').strpath
```

**Verification:**
```python
assert out.outputs.erosion == ['300.1', '5', '0.3']
```

### Step 4: Assign reader = utility.CSVReader(...)

```python
reader = utility.CSVReader(delimiter='\t')
```

**Verification:**
```python
assert out.outputs.column_0 == ['foo', 'bar', 'baz']
```

### Step 5: Call fid.writelines()

```python
fid.writelines(lines)
```

**Verification:**
```python
assert out.outputs.column_1 == ['hello', 'world', 'goodbye']
```

### Step 6: Call fid.flush()

```python
fid.flush()
```

**Verification:**
```python
assert out.outputs.column_2 == ['300.1', '5', '0.3']
```

### Step 7: Assign reader.inputs.in_file = name

```python
reader.inputs.in_file = name
```

### Step 8: Assign out = reader.run(...)

```python
out = reader.run()
```

### Step 9: Call fid.write()

```python
fid.write(header)
```

### Step 10: Assign reader.inputs.header = True

```python
reader.inputs.header = True
```

**Verification:**
```python
assert out.outputs.files == ['foo', 'bar', 'baz']
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
header = 'files\tlabels\terosion\n'
lines = ['foo\thello\t300.1\n', 'bar\tworld\t5\n', 'baz\tgoodbye\t0.3\n']
for x in range(2):
    name = tmpdir.join('testfile.csv').strpath
    with open(name, 'w') as fid:
        reader = utility.CSVReader(delimiter='\t')
        if x % 2 == 0:
            fid.write(header)
            reader.inputs.header = True
        fid.writelines(lines)
        fid.flush()
        reader.inputs.in_file = name
        out = reader.run()
        if x % 2 == 0:
            assert out.outputs.files == ['foo', 'bar', 'baz']
            assert out.outputs.labels == ['hello', 'world', 'goodbye']
            assert out.outputs.erosion == ['300.1', '5', '0.3']
        else:
            assert out.outputs.column_0 == ['foo', 'bar', 'baz']
            assert out.outputs.column_1 == ['hello', 'world', 'goodbye']
            assert out.outputs.column_2 == ['300.1', '5', '0.3']
```

## Next Steps


---

*Source: test_csv.py:47 | Complexity: Advanced | Last updated: 2026-05-18*