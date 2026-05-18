# How To: Format Key Value Table

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test format key value table

## Prerequisites

**Required Modules:**
- `importlib`
- `inspect`
- `logging`
- `pathlib`
- `shutil`
- `sys`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.data.fetcher`
- `dipy.direction.peaks`
- `dipy.io.image`
- `dipy.io.peaks`
- `dipy.io.streamline`
- `dipy.io.utils`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`
- `dipy.workflows.base`
- `dipy.workflows.io`


## Step-by-Step Guide

### Step 1: Assign table = format_key_value_table(...)

```python
table = format_key_value_table({'foo': 'Foo description', 'bar': 'x' * 200}, key_header='Dataset', value_header='Description')
```

### Step 2: Assign table_lines = table.splitlines(...)

```python
table_lines = table.splitlines()
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(any(('Dataset' in line for line in table_lines)), True)
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(any(('Description' in line for line in table_lines)), True)
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(any(('foo' in line for line in table_lines)), True)
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(any(('Foo description' in line for line in table_lines)), True)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(sum(('x' in line for line in table_lines)) > 1, True)
```

### Step 8: Assign table_sorted = format_key_value_table(...)

```python
table_sorted = format_key_value_table({'zebra': 'last', 'apple': 'first'}, key_header='Key', value_header='Value')
```

### Step 9: Assign sorted_lines = value

```python
sorted_lines = [line for line in table_sorted.splitlines() if 'apple' in line or 'zebra' in line]
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(len(sorted_lines), 2)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal('apple' in sorted_lines[0], True)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal('zebra' in sorted_lines[1], True)
```

### Step 13: Assign table_unsorted = format_key_value_table(...)

```python
table_unsorted = format_key_value_table({'zebra': 'last', 'apple': 'first'}, key_header='Key', value_header='Value', sort=False)
```

### Step 14: Assign unsorted_lines = value

```python
unsorted_lines = [line for line in table_unsorted.splitlines() if 'apple' in line or 'zebra' in line]
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(len(unsorted_lines), 2)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal('zebra' in unsorted_lines[0], True)
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal('apple' in unsorted_lines[1], True)
```

### Step 18: Assign multiline = format_key_value_table(...)

```python
multiline = format_key_value_table({'key': 'first line\nsecond line'}, key_header='Key', value_header='Value')
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(any(('first line' in line for line in multiline.splitlines())), True)
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(any(('second line' in line for line in multiline.splitlines())), True)
```

### Step 21: Assign indented = format_key_value_table(...)

```python
indented = format_key_value_table({'key': '    indented text'}, key_header='Key', value_header='Value')
```

### Step 22: Call npt.assert_equal()

```python
npt.assert_equal(any(('    indented text' in line for line in indented.splitlines())), True)
```


## Complete Example

```python
# Workflow
table = format_key_value_table({'foo': 'Foo description', 'bar': 'x' * 200}, key_header='Dataset', value_header='Description')
table_lines = table.splitlines()
npt.assert_equal(any(('Dataset' in line for line in table_lines)), True)
npt.assert_equal(any(('Description' in line for line in table_lines)), True)
npt.assert_equal(any(('foo' in line for line in table_lines)), True)
npt.assert_equal(any(('Foo description' in line for line in table_lines)), True)
npt.assert_equal(sum(('x' in line for line in table_lines)) > 1, True)
table_sorted = format_key_value_table({'zebra': 'last', 'apple': 'first'}, key_header='Key', value_header='Value')
sorted_lines = [line for line in table_sorted.splitlines() if 'apple' in line or 'zebra' in line]
npt.assert_equal(len(sorted_lines), 2)
npt.assert_equal('apple' in sorted_lines[0], True)
npt.assert_equal('zebra' in sorted_lines[1], True)
table_unsorted = format_key_value_table({'zebra': 'last', 'apple': 'first'}, key_header='Key', value_header='Value', sort=False)
unsorted_lines = [line for line in table_unsorted.splitlines() if 'apple' in line or 'zebra' in line]
npt.assert_equal(len(unsorted_lines), 2)
npt.assert_equal('zebra' in unsorted_lines[0], True)
npt.assert_equal('apple' in unsorted_lines[1], True)
multiline = format_key_value_table({'key': 'first line\nsecond line'}, key_header='Key', value_header='Value')
npt.assert_equal(any(('first line' in line for line in multiline.splitlines())), True)
npt.assert_equal(any(('second line' in line for line in multiline.splitlines())), True)
indented = format_key_value_table({'key': '    indented text'}, key_header='Key', value_header='Value')
npt.assert_equal(any(('    indented text' in line for line in indented.splitlines())), True)
```

## Next Steps


---

*Source: test_io.py:223 | Complexity: Advanced | Last updated: 2026-05-18*