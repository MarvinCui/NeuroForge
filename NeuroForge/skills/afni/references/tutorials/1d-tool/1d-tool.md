# How To: 1D Tool

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 1d tool

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = data.outdir / '1d_tool_output.1d'
```

### Step 2: Assign cmd = '\n    1d_tool.py\n    -set_run_lengths 150 150 150\n    -index_to_run_tr 324\n    > {outfile}\n    '

```python
cmd = '\n    1d_tool.py\n    -set_run_lengths 150 150 150\n    -index_to_run_tr 324\n    > {outfile}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd)
```

### Step 5: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data

# Workflow
outfile = data.outdir / '1d_tool_output.1d'
cmd = '\n    1d_tool.py\n    -set_run_lengths 150 150 150\n    -index_to_run_tr 324\n    > {outfile}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_1d_tool.py:7 | Complexity: Intermediate | Last updated: 2026-05-18*