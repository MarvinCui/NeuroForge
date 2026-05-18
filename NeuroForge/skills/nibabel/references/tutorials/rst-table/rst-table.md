# How To: Rst Table

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rst table

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `rstutils`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
R, C = (3, 4)
```

**Verification:**
```python
assert rst_table(cell_values) == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
```

### Step 2: Assign cell_values = np.arange.reshape(...)

```python
cell_values = np.arange(R * C).reshape((R, C))
```

**Verification:**
```python
assert rst_table(cell_values, ['a', 'b', 'c']) == '+---+--------+--------+--------+--------+\n|   | col[0] | col[1] | col[2] | col[3] |\n+===+========+========+========+========+\n| a |  0.00  |  1.00  |  2.00  |  3.00  |\n| b |  4.00  |  5.00  |  6.00  |  7.00  |\n| c |  8.00  |  9.00  | 10.00  | 11.00  |\n+---+--------+--------+--------+--------+'
```

### Step 3: Assign cell_values_back = unknown.reshape(...)

```python
cell_values_back = np.arange(R * C)[::-1].reshape((R, C))
```

**Verification:**
```python
assert rst_table(cell_values, None, ['1', '2', '3', '4']) == '+--------+-------+-------+-------+-------+\n|        |   1   |   2   |   3   |   4   |\n+========+=======+=======+=======+=======+\n| row[0] |  0.00 |  1.00 |  2.00 |  3.00 |\n| row[1] |  4.00 |  5.00 |  6.00 |  7.00 |\n| row[2] |  8.00 |  9.00 | 10.00 | 11.00 |\n+--------+-------+-------+-------+-------+'
```

### Step 4: Assign cell_3d = np.dstack(...)

```python
cell_3d = np.dstack((cell_values, cell_values_back))
```

**Verification:**
```python
assert rst_table(cell_values, title='A title') == '*******\nA title\n*******\n\n+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
```

### Step 5: Assign formats = dict(...)

```python
formats = dict(down='!', along='_', thick_long='~', cross='%', title_heading='#')
```

**Verification:**
```python
assert rst_table(cell_values, val_fmt='{0}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0      | 1      | 2      | 3      |\n| row[1] | 4      | 5      | 6      | 7      |\n| row[2] | 8      | 9      | 10     | 11     |\n+--------+--------+--------+--------+--------+'
```

### Step 6: Assign unknown = '!'

```python
formats['funny_value'] = '!'
```

**Verification:**
```python
assert rst_table(cell_3d, val_fmt='{0[0]}-{0[1]}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0-11   | 1-10   | 2-9    | 3-8    |\n| row[1] | 4-7    | 5-6    | 6-5    | 7-4    |\n| row[2] | 8-3    | 9-2    | 10-1   | 11-0   |\n+--------+--------+--------+--------+--------+'
```

### Step 7: Call rst_table()

```python
rst_table(cell_values, ['a', 'b'])
```

**Verification:**
```python
assert rst_table(cell_values, title='A title', format_chars=formats) == '#######\nA title\n#######\n\n%________%________%________%________%________%\n!        ! col[0] ! col[1] ! col[2] ! col[3] !\n%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%\n! row[0] !  0.00  !  1.00  !  2.00  !  3.00  !\n! row[1] !  4.00  !  5.00  !  6.00  !  7.00  !\n! row[2] !  8.00  !  9.00  ! 10.00  ! 11.00  !\n%________%________%________%________%________%'
```

### Step 8: Call rst_table()

```python
rst_table(cell_values, ['a', 'b', 'c', 'd'])
```

### Step 9: Call rst_table()

```python
rst_table(cell_values, None, ['1', '2', '3'])
```

### Step 10: Call rst_table()

```python
rst_table(cell_values, None, list('12345'))
```

### Step 11: Call rst_table()

```python
rst_table(cell_values, title='A title', format_chars=formats)
```


## Complete Example

```python
# Workflow
R, C = (3, 4)
cell_values = np.arange(R * C).reshape((R, C))
assert rst_table(cell_values) == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, ['a', 'b', 'c']) == '+---+--------+--------+--------+--------+\n|   | col[0] | col[1] | col[2] | col[3] |\n+===+========+========+========+========+\n| a |  0.00  |  1.00  |  2.00  |  3.00  |\n| b |  4.00  |  5.00  |  6.00  |  7.00  |\n| c |  8.00  |  9.00  | 10.00  | 11.00  |\n+---+--------+--------+--------+--------+'
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b'])
with pytest.raises(ValueError):
    rst_table(cell_values, ['a', 'b', 'c', 'd'])
assert rst_table(cell_values, None, ['1', '2', '3', '4']) == '+--------+-------+-------+-------+-------+\n|        |   1   |   2   |   3   |   4   |\n+========+=======+=======+=======+=======+\n| row[0] |  0.00 |  1.00 |  2.00 |  3.00 |\n| row[1] |  4.00 |  5.00 |  6.00 |  7.00 |\n| row[2] |  8.00 |  9.00 | 10.00 | 11.00 |\n+--------+-------+-------+-------+-------+'
with pytest.raises(ValueError):
    rst_table(cell_values, None, ['1', '2', '3'])
with pytest.raises(ValueError):
    rst_table(cell_values, None, list('12345'))
assert rst_table(cell_values, title='A title') == '*******\nA title\n*******\n\n+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] |  0.00  |  1.00  |  2.00  |  3.00  |\n| row[1] |  4.00  |  5.00  |  6.00  |  7.00  |\n| row[2] |  8.00  |  9.00  | 10.00  | 11.00  |\n+--------+--------+--------+--------+--------+'
assert rst_table(cell_values, val_fmt='{0}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0      | 1      | 2      | 3      |\n| row[1] | 4      | 5      | 6      | 7      |\n| row[2] | 8      | 9      | 10     | 11     |\n+--------+--------+--------+--------+--------+'
cell_values_back = np.arange(R * C)[::-1].reshape((R, C))
cell_3d = np.dstack((cell_values, cell_values_back))
assert rst_table(cell_3d, val_fmt='{0[0]}-{0[1]}') == '+--------+--------+--------+--------+--------+\n|        | col[0] | col[1] | col[2] | col[3] |\n+========+========+========+========+========+\n| row[0] | 0-11   | 1-10   | 2-9    | 3-8    |\n| row[1] | 4-7    | 5-6    | 6-5    | 7-4    |\n| row[2] | 8-3    | 9-2    | 10-1   | 11-0   |\n+--------+--------+--------+--------+--------+'
formats = dict(down='!', along='_', thick_long='~', cross='%', title_heading='#')
assert rst_table(cell_values, title='A title', format_chars=formats) == '#######\nA title\n#######\n\n%________%________%________%________%________%\n!        ! col[0] ! col[1] ! col[2] ! col[3] !\n%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%~~~~~~~~%\n! row[0] !  0.00  !  1.00  !  2.00  !  3.00  !\n! row[1] !  4.00  !  5.00  !  6.00  !  7.00  !\n! row[2] !  8.00  !  9.00  ! 10.00  ! 11.00  !\n%________%________%________%________%________%'
formats['funny_value'] = '!'
with pytest.raises(ValueError):
    rst_table(cell_values, title='A title', format_chars=formats)
```

## Next Steps


---

*Source: test_rstutils.py:9 | Complexity: Advanced | Last updated: 2026-05-18*