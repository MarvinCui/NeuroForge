# How To: Formatting

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test formatting

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `psychopy`
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual`
- `psychopy.visual`
- `psychopy.tools.fontmanager`
- `pytest`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = [{'text': 'This contains ***bold italic*** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bolditalic'}, {'text': 'This contains **bold** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bold'}, {'text': 'This contains *italic* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'italic'}, {'text': 'This contains \\*escaped\\* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'escaped'}, {'text': 'This contains [color=red]colorful[/color] text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'color'}, {'text': 'This text contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'md'}, {'text': 'השועל [color=brown]החום[/color] המהיר קופץ **מעל** הכלב ה*עצלן*.', 'syntax': 'md', 'languageStyle': 'RTL', 'screenshot': 'all'}, {'text': 'This text contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'html', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'html'}, {'text': 'השועל <span style="color: brown">החום</span> המהיר קופץ <b>מעל</b> הכלב ה<i>עצלן</i>.', 'syntax': 'html', 'languageStyle': 'RTL', 'screenshot': 'all'}]
```

### Step 2: Call self.textbox.fontMGR.addGoogleFont()

```python
self.textbox.fontMGR.addGoogleFont('Noto Sans Hebrew')
```

### Step 3: Call self.textbox.fontMGR.addGoogleFont()

```python
self.textbox.fontMGR.addGoogleFont('Noto Sans')
```

### Step 4: Assign self.textbox.languageStyle = value

```python
self.textbox.languageStyle = case['languageStyle']
```

### Step 5: Assign self.textbox.formattingSyntax = value

```python
self.textbox.formattingSyntax = case['syntax']
```

### Step 6: Assign self.textbox.text = value

```python
self.textbox.text = case['text']
```

### Step 7: Call self.win.flip()

```python
self.win.flip()
```

### Step 8: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 9: Assign filename = value

```python
filename = f'{type(self).__name__}_textbox_formatting_%(screenshot)s_%(syntax)s_%(languageStyle)s.png' % case
```

### Step 10: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

### Step 11: Assign self.textbox.font = 'Noto Sans Hebrew'

```python
self.textbox.font = 'Noto Sans Hebrew'
```

### Step 12: Assign self.textbox.font = 'Noto Sans'

```python
self.textbox.font = 'Noto Sans'
```


## Complete Example

```python
# Workflow
cases = [{'text': 'This contains ***bold italic*** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bolditalic'}, {'text': 'This contains **bold** text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'bold'}, {'text': 'This contains *italic* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'italic'}, {'text': 'This contains \\*escaped\\* text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'escaped'}, {'text': 'This contains [color=red]colorful[/color] text', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'color'}, {'text': 'This text contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'md', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains ***bold italic***, **bold**, *italic*, \\*escaped\\*, and [color=red]colorful[/color] text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'md'}, {'text': 'השועל [color=brown]החום[/color] המהיר קופץ **מעל** הכלב ה*עצלן*.', 'syntax': 'md', 'languageStyle': 'RTL', 'screenshot': 'all'}, {'text': 'This text contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'html', 'languageStyle': 'LTR', 'screenshot': 'all'}, {'text': 'This text contains no formatting, but looks like it contains <b><i>bold italic</i></b>, <i><b>italic bold</b></i>, <b>bold</b>, <i>italic</i>, <div>div wrapped</div> and <span style="color: red">colorful</span> text.', 'syntax': 'raw', 'languageStyle': 'LTR', 'screenshot': 'html'}, {'text': 'השועל <span style="color: brown">החום</span> המהיר קופץ <b>מעל</b> הכלב ה<i>עצלן</i>.', 'syntax': 'html', 'languageStyle': 'RTL', 'screenshot': 'all'}]
self.textbox.fontMGR.addGoogleFont('Noto Sans Hebrew')
self.textbox.fontMGR.addGoogleFont('Noto Sans')
for case in cases:
    if case['languageStyle'] == 'RTL':
        self.textbox.font = 'Noto Sans Hebrew'
    else:
        self.textbox.font = 'Noto Sans'
    self.textbox.languageStyle = case['languageStyle']
    self.textbox.formattingSyntax = case['syntax']
    self.textbox.text = case['text']
    self.win.flip()
    self.textbox.draw()
    filename = f'{type(self).__name__}_textbox_formatting_%(screenshot)s_%(syntax)s_%(languageStyle)s.png' % case
    utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## Next Steps


---

*Source: test_textbox.py:197 | Complexity: Advanced | Last updated: 2026-05-18*