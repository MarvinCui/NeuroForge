# How To: Param Str

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that params convert to str as expected in both Python and JS

## Prerequisites

**Required Modules:**
- `re`
- `inspect`
- `pathlib`
- `utils`
- `psychopy`
- `psychopy.experiment`


## Step-by-Step Guide

### Step 1: '\n    Test that params convert to str as expected in both Python and JS\n    '

```python
'\n    Test that params convert to str as expected in both Python and JS\n    '
```

**Verification:**
```python
assert re.fullmatch(case['py'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['py']}`, but it was `{case['obj']}`"
```

### Step 2: Assign sl = '\\'

```python
sl = '\\'
```

**Verification:**
```python
assert re.fullmatch(case['js'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['js']}`, but it was `{case['obj']}`"
```

### Step 3: Assign cases = value

```python
cases = [{'obj': Param('Hello there', 'str'), 'py': f'{_q}Hello there{_q}', 'js': f'{_q}Hello there{_q}'}, {'obj': Param('\\, | or /', 'str', canBePath=False), 'py': f'{_q}{_sl}, \\| or /{_q}', 'js': f'{_q}{_sl}, \\| or /{_q}'}, {'obj': Param('$win.color', 'str'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('1', 'int'), 'py': f'1', 'js': f'1'}, {'obj': Param('1', 'num'), 'py': f'1.0', 'js': f'1.0'}, {'obj': Param('C:/Downloads/file.ext', 'file'), 'py': f'{_q}C:/Downloads/file.ext{_q}', 'js': f'{_q}C:/Downloads/file.ext{_q}'}, {'obj': Param('C:/Downloads/file.csv', 'table'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('red', 'color'), 'py': f'{_q}red{_q}', 'js': f'{_q}red{_q}'}, {'obj': Param('0.7, 0.7, 0.7', 'color'), 'py': f'{_lb}0.7, 0.7, 0.7{_rb}', 'js': f'{_lb}0.7, 0.7, 0.7{_rb}'}, {'obj': Param('win.color', 'code'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('for x in y:\n\tprint(y)', 'extendedCode'), 'py': f'for x in y:\n\tprint{_lb}y{_rb}', 'js': f'for x in y:\n\tprint{_lb}y{_rb}'}, {'obj': Param('1, 2, 3', 'list'), 'py': f'{_lb}1, 2, 3{_rb}', 'js': f'{_lb}1, 2, 3{_rb}'}, {'obj': Param(__file__, 'str'), 'py': f"{_q}{__file__.replace(sl, '/')}{_q}", 'js': f"{_q}{__file__.replace(sl, '/')}{_q}"}, {'obj': Param('C:\\\\Downloads\\file.csv', 'str'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('C:\\\\Downloads\\_file.csv', 'str'), 'py': f'{_q}C:/Downloads/_file.csv{_q}', 'js': f'{_q}C:/Downloads/_file.csv{_q}'}, {'obj': Param('This costs \\$4.20', 'str'), 'py': f'{_q}This costs {_d}4.20{_q}', 'js': f'{_q}This costs {_d}4.20{_q}'}, {'obj': Param('This \\ that', 'str'), 'py': f'{_q}This {_sl} that{_q}', 'js': f'{_q}This {_sl} that{_q}'}, {'obj': Param('variableName', 'code'), 'py': f'variableName', 'js': f'variableName'}, {'obj': Param('$letterColor', 'color'), 'py': f'letterColor', 'js': f'letterColor'}, {'obj': Param('"left", "down", "right"', 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("'left', 'down', 'right'", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("('left', 'down', 'right')", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("['left', 'down', 'right']", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param('"left"', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('["left"]', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('$left', 'list'), 'py': 'left', 'js': 'left'}, {'obj': Param('path\\to\\resource', 'str', canBePath=True), 'py': "'path/to/resource'", 'js': "'path/to/resource'"}, {'obj': Param("$Math.E+'$'", 'str'), 'py': "Math\\.E\\+'\\$'", 'js': '\\(Math.E \\+ \\"\\$\\"\\)'}]
```

### Step 4: Assign initTarget = value

```python
initTarget = exputils.scriptTarget
```

### Step 5: Assign exputils.scriptTarget = initTarget

```python
exputils.scriptTarget = initTarget
```

### Step 6: Assign exputils.scriptTarget = 'PsychoPy'

```python
exputils.scriptTarget = 'PsychoPy'
```

**Verification:**
```python
assert re.fullmatch(case['py'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['py']}`, but it was `{case['obj']}`"
```

### Step 7: Assign exputils.scriptTarget = 'PsychoJS'

```python
exputils.scriptTarget = 'PsychoJS'
```

**Verification:**
```python
assert re.fullmatch(case['js'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['js']}`, but it was `{case['obj']}`"
```


## Complete Example

```python
# Workflow
'\n    Test that params convert to str as expected in both Python and JS\n    '
sl = '\\'
cases = [{'obj': Param('Hello there', 'str'), 'py': f'{_q}Hello there{_q}', 'js': f'{_q}Hello there{_q}'}, {'obj': Param('\\, | or /', 'str', canBePath=False), 'py': f'{_q}{_sl}, \\| or /{_q}', 'js': f'{_q}{_sl}, \\| or /{_q}'}, {'obj': Param('$win.color', 'str'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('1', 'int'), 'py': f'1', 'js': f'1'}, {'obj': Param('1', 'num'), 'py': f'1.0', 'js': f'1.0'}, {'obj': Param('C:/Downloads/file.ext', 'file'), 'py': f'{_q}C:/Downloads/file.ext{_q}', 'js': f'{_q}C:/Downloads/file.ext{_q}'}, {'obj': Param('C:/Downloads/file.csv', 'table'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('red', 'color'), 'py': f'{_q}red{_q}', 'js': f'{_q}red{_q}'}, {'obj': Param('0.7, 0.7, 0.7', 'color'), 'py': f'{_lb}0.7, 0.7, 0.7{_rb}', 'js': f'{_lb}0.7, 0.7, 0.7{_rb}'}, {'obj': Param('win.color', 'code'), 'py': f'win.color', 'js': f'psychoJS.window.color'}, {'obj': Param('for x in y:\n\tprint(y)', 'extendedCode'), 'py': f'for x in y:\n\tprint{_lb}y{_rb}', 'js': f'for x in y:\n\tprint{_lb}y{_rb}'}, {'obj': Param('1, 2, 3', 'list'), 'py': f'{_lb}1, 2, 3{_rb}', 'js': f'{_lb}1, 2, 3{_rb}'}, {'obj': Param(__file__, 'str'), 'py': f"{_q}{__file__.replace(sl, '/')}{_q}", 'js': f"{_q}{__file__.replace(sl, '/')}{_q}"}, {'obj': Param('C:\\\\Downloads\\file.csv', 'str'), 'py': f'{_q}C:/Downloads/file.csv{_q}', 'js': f'{_q}C:/Downloads/file.csv{_q}'}, {'obj': Param('C:\\\\Downloads\\_file.csv', 'str'), 'py': f'{_q}C:/Downloads/_file.csv{_q}', 'js': f'{_q}C:/Downloads/_file.csv{_q}'}, {'obj': Param('This costs \\$4.20', 'str'), 'py': f'{_q}This costs {_d}4.20{_q}', 'js': f'{_q}This costs {_d}4.20{_q}'}, {'obj': Param('This \\ that', 'str'), 'py': f'{_q}This {_sl} that{_q}', 'js': f'{_q}This {_sl} that{_q}'}, {'obj': Param('variableName', 'code'), 'py': f'variableName', 'js': f'variableName'}, {'obj': Param('$letterColor', 'color'), 'py': f'letterColor', 'js': f'letterColor'}, {'obj': Param('"left", "down", "right"', 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("'left', 'down', 'right'", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("('left', 'down', 'right')", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param("['left', 'down', 'right']", 'list'), 'py': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}', 'js': f'{_lb}{_q}left{_q}, {_q}down{_q}, {_q}right{_q}{_rb}'}, {'obj': Param('"left"', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('["left"]', 'list'), 'py': f'{_lb}{_q}left{_q}{_rb}'}, {'obj': Param('$left', 'list'), 'py': 'left', 'js': 'left'}, {'obj': Param('path\\to\\resource', 'str', canBePath=True), 'py': "'path/to/resource'", 'js': "'path/to/resource'"}, {'obj': Param("$Math.E+'$'", 'str'), 'py': "Math\\.E\\+'\\$'", 'js': '\\(Math.E \\+ \\"\\$\\"\\)'}]
initTarget = exputils.scriptTarget
for case in cases:
    if 'py' in case:
        exputils.scriptTarget = 'PsychoPy'
        assert re.fullmatch(case['py'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['py']}`, but it was `{case['obj']}`"
    if 'js' in case:
        exputils.scriptTarget = 'PsychoJS'
        assert re.fullmatch(case['js'], str(case['obj'])), f"`{repr(case['obj'])}` should match the regex `{case['js']}`, but it was `{case['obj']}`"
exputils.scriptTarget = initTarget
```

## Next Steps


---

*Source: test_params.py:167 | Complexity: Intermediate | Last updated: 2026-05-18*