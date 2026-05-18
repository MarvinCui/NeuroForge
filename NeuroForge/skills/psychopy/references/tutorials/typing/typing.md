# How To: Typing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that continuous typing doesn't break anything

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

### Step 1: "Check that continuous typing doesn't break anything"

```python
"Check that continuous typing doesn't break anything"
```

### Step 2: Assign self.textbox.color = 'white'

```python
self.textbox.color = 'white'
```

### Step 3: Assign self.textbox.fillColor = None

```python
self.textbox.fillColor = None
```

### Step 4: Assign self.textbox.borderColor = None

```python
self.textbox.borderColor = None
```

### Step 5: Assign wasEditable = value

```python
wasEditable = self.textbox.editable
```

### Step 6: Assign self.textbox.editable = True

```python
self.textbox.editable = True
```

### Step 7: Assign exemplars = value

```python
exemplars = [{'text': '', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'test←←←←', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_pangram.png'}, {'text': 'ther◀◀◀◀Hello ▶▶▶▶e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navLR.png'}, {'text': 'Hello←o there←e◀◀◀→e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navDel.png'}, {'text': 'Hello\nthere', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_newline.png'}]
```

### Step 8: Assign tykes = value

```python
tykes = [{'text': 'i need a word which will go off the page, antidisestablishmentarianism is a very long word', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_longWord.png'}]
```

### Step 9: Assign self.textbox.editable = wasEditable

```python
self.textbox.editable = wasEditable
```

### Step 10: Assign self.textbox.font = value

```python
self.textbox.font = case['font']
```

### Step 11: Assign self.textbox.text = ''

```python
self.textbox.text = ''
```

### Step 12: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 13: Call self.win.flip()

```python
self.win.flip()
```

### Step 14: Call self.win.flip()

```python
self.win.flip()
```

### Step 15: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 16: Call self.textbox.caret.draw()

```python
self.textbox.caret.draw(override=True)
```

### Step 17: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / case['screenshot'], self.win, crit=20)
```

### Step 18: Call self.textbox._onCursorKeys()

```python
self.textbox._onCursorKeys('MOTION_LEFT')
```

### Step 19: Call self.textbox._onCursorKeys()

```python
self.textbox._onCursorKeys('MOTION_RIGHT')
```

### Step 20: Call self.textbox._onCursorKeys()

```python
self.textbox._onCursorKeys('MOTION_BACKSPACE')
```

### Step 21: Call self.textbox._onCursorKeys()

```python
self.textbox._onCursorKeys('MOTION_DELETE')
```

### Step 22: Call self.textbox._onText()

```python
self.textbox._onText(letter)
```


## Complete Example

```python
# Workflow
"Check that continuous typing doesn't break anything"
self.textbox.color = 'white'
self.textbox.fillColor = None
self.textbox.borderColor = None
wasEditable = self.textbox.editable
self.textbox.editable = True
exemplars = [{'text': '', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'test←←←←', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_blank.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_pangram.png'}, {'text': 'ther◀◀◀◀Hello ▶▶▶▶e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navLR.png'}, {'text': 'Hello←o there←e◀◀◀→e', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_navDel.png'}, {'text': 'Hello\nthere', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_newline.png'}]
tykes = [{'text': 'i need a word which will go off the page, antidisestablishmentarianism is a very long word', 'font': 'Noto Sans', 'screenshot': 'textbox_typing_longWord.png'}]
for case in exemplars + tykes:
    self.textbox.font = case['font']
    self.textbox.text = ''
    for letter in case['text']:
        if letter == '◀':
            self.textbox._onCursorKeys('MOTION_LEFT')
        elif letter == '▶':
            self.textbox._onCursorKeys('MOTION_RIGHT')
        elif letter == '←':
            self.textbox._onCursorKeys('MOTION_BACKSPACE')
        elif letter == '→':
            self.textbox._onCursorKeys('MOTION_DELETE')
        else:
            self.textbox._onText(letter)
        self.textbox.draw()
        self.win.flip()
    if case['screenshot']:
        self.win.flip()
        self.textbox.draw()
        self.textbox.caret.draw(override=True)
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / case['screenshot'], self.win, crit=20)
self.textbox.editable = wasEditable
```

## Next Steps


---

*Source: test_textbox.py:399 | Complexity: Advanced | Last updated: 2026-05-18*