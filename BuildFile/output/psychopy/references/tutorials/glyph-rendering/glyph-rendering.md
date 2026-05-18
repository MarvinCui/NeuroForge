# How To: Glyph Rendering

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test glyph rendering

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

### Step 1: Assign self.textbox.colorSpace = 'rgb'

```python
self.textbox.colorSpace = 'rgb'
```

### Step 2: Assign self.textbox.color = 'white'

```python
self.textbox.color = 'white'
```

### Step 3: Assign self.textbox.fillColor = value

```python
self.textbox.fillColor = (0, 0, 0)
```

### Step 4: Assign self.textbox.borderColor = None

```python
self.textbox.borderColor = None
```

### Step 5: Assign self.textbox.opacity = 1

```python
self.textbox.opacity = 1
```

### Step 6: Assign exemplars = value

```python
exemplars = [{'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_1.png'}, {'text': 'ə saɪkəʊpaɪ zɛlət nəʊz ə smidge ɒv wx, bʌt ˈʤɑːvəskrɪpt ɪz ðə ˈkwɛsʧən', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_2.png'}, {'text': '아 프시초피 제알롣 크노W스 아 s믿게 오f wx, 붇 자v앗c립t 잇 테 q왯디온', 'font': 'Noto Sans KR', 'size': 16, 'screenshot': 'exemplar_3.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Indie Flower', 'size': 16, 'screenshot': 'exemplar_4.png'}]
```

### Step 7: Assign tykes = value

```python
tykes = [{'text': 'कोशिकायें', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'tyke_1.png'}, {'text': 'ขาว แดง เขียว เหลือง ชมพู ม่วง เทา', 'font': 'Niramit', 'size': 16, 'screenshot': 'tyke_2.png'}, {'text': 'โฬิปื้ด็ลู', 'font': 'Niramit', 'size': 36, 'screenshot': 'cutoff_top.png'}]
```

### Step 8: Call self.textbox.fontMGR.addGoogleFont()

```python
self.textbox.fontMGR.addGoogleFont(font)
```

### Step 9: Call self.textbox.reset()

```python
self.textbox.reset()
```

### Step 10: Call self.textbox.fontMGR.addGoogleFont()

```python
self.textbox.fontMGR.addGoogleFont(case['font'])
```

### Step 11: Assign self.textbox.letterHeight = layout.Size(...)

```python
self.textbox.letterHeight = layout.Size(case['size'], 'pix', self.win)
```

### Step 12: Assign self.textbox.font = value

```python
self.textbox.font = case['font']
```

### Step 13: Assign self.textbox.text = value

```python
self.textbox.text = case['text']
```

### Step 14: Call self.win.flip()

```python
self.win.flip()
```

### Step 15: Call self.textbox.draw()

```python
self.textbox.draw()
```

### Step 16: Assign filename = unknown.format(...)

```python
filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
```

### Step 17: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```


## Complete Example

```python
# Workflow
self.textbox.colorSpace = 'rgb'
self.textbox.color = 'white'
self.textbox.fillColor = (0, 0, 0)
self.textbox.borderColor = None
self.textbox.opacity = 1
for font in ['Noto Sans', 'Noto Sans HK', 'Noto Sans JP', 'Noto Sans KR', 'Noto Sans SC', 'Noto Sans TC', 'Niramit', 'Indie Flower']:
    self.textbox.fontMGR.addGoogleFont(font)
exemplars = [{'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_1.png'}, {'text': 'ə saɪkəʊpaɪ zɛlət nəʊz ə smidge ɒv wx, bʌt ˈʤɑːvəskrɪpt ɪz ðə ˈkwɛsʧən', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'exemplar_2.png'}, {'text': '아 프시초피 제알롣 크노W스 아 s믿게 오f wx, 붇 자v앗c립t 잇 테 q왯디온', 'font': 'Noto Sans KR', 'size': 16, 'screenshot': 'exemplar_3.png'}, {'text': 'A PsychoPy zealot knows a smidge of wx, but JavaScript is the question.', 'font': 'Indie Flower', 'size': 16, 'screenshot': 'exemplar_4.png'}]
tykes = [{'text': 'कोशिकायें', 'font': 'Noto Sans', 'size': 16, 'screenshot': 'tyke_1.png'}, {'text': 'ขาว แดง เขียว เหลือง ชมพู ม่วง เทา', 'font': 'Niramit', 'size': 16, 'screenshot': 'tyke_2.png'}, {'text': 'โฬิปื้ด็ลู', 'font': 'Niramit', 'size': 36, 'screenshot': 'cutoff_top.png'}]
for case in exemplars + tykes:
    self.textbox.reset()
    self.textbox.fontMGR.addGoogleFont(case['font'])
    self.textbox.letterHeight = layout.Size(case['size'], 'pix', self.win)
    self.textbox.font = case['font']
    self.textbox.text = case['text']
    self.win.flip()
    self.textbox.draw()
    if case['screenshot']:
        filename = 'textbox_{}_{}'.format(self.textbox._lineBreaking, case['screenshot'])
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

## Next Steps


---

*Source: test_textbox.py:45 | Complexity: Advanced | Last updated: 2026-05-18*